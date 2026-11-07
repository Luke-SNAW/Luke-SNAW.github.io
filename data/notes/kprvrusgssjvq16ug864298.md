
> Manish Sharma
>
> https://medium.com/aws-tip/understanding-nestjs-architecture-f257d054211d

NestJS is a NodeJs framework built on top of ExpressJs and is used for building efficient, scalable, loosely coupled, testable and easily maintainable server side web applications using architecture principles in mind.

> The problem NestJs trying to solve is that of architecture. As [Lee Barker](https://madecurious.com/curiosities/the-benefits-of-taking-an-architectural-approach-to-software-development/) says: Architectural approach promotes a whole heap of things from good design through to the early identification of potential risks, and gives stakeholders more clarity, among other things

**Hello NestJS**

The simplest approach is to create a Controller doing all things: from validation to request-processing to handling business logic to interacting with data base and so on.

![Fat Ugly Controller](./assets/images/javascript/nestjs__fat-ugly-controller.avif)

Fat Ugly Controller

```js
/*
  /simple/convert/12
*/
import { Controller, Get, Param } from "@nestjs/common"
@Controller("simple")
export class SimpleController {
  @Get("/convert/:inr")
  convert(@Param("inr") inr: number) {
    return inr * 80
  }
}
```

This is FAT controller approach, [NOT recommended](https://medium.com/@steadweb/the-fat-controller-and-its-misuse-part-1-710bc38fe19) at all. Why ?

## Services

**Rule# 1:** Business logic should be delegated to a separate entity known as service.

![Controller using Service](./assets/images/javascript/nestjs__controller-using-service.avif)

Controller using Service

Let’s create a service first:

```js
import { Injectable } from "@nestjs/common"
@Injectable()
export class ConverterService {
  convert(inr: number): number {
    return inr * 80
  }
}
```

Services have to “Injectable” and has be registered in Module under providers section :

```js
providers: [ConverterService],
```

NestJS follows dependency injection of [SOLID principles](https://medium.com/backticks-tildes/the-s-o-l-i-d-principles-in-pictures-b34ce2f1e898). We do not want Controller to instantiate services to be used. Injectable reduces the dependency of Controller on dependent services. NestJs is responsible for “instantiating” service as per requirement. Inside controller we have used constructor for service injection.

```js
import { Controller, Get, Param } from '@nestjs/common';
import { ConverterService } from './converter.service';
@Controller('service')
export class ServiceController {
  /* ConverterService is Injectable, so NestJS handles task of instantiation*/
  constructor(private readonly converterService: ConverterService) {}

  @Get('/convert/:inr')
  convert(@Param('inr') inr: number): number {
    return this.converterService.convert(inr);
  }
}
```

So far so good. But what about Validation ?  
Executing [**http://127.0.0.1:3000/service/convert/**](http://127.0.0.1:3000/service/convert/aa)**12** will work, but [**http://127.0.0.1:3000/service/convert/aa**](http://127.0.0.1:3000/service/convert/aa) won’t. It will return NaN (Not a number). What we are missing is Validation layer. Implementing validation logic inside controller will again turn it into a FAT UGLY Controller. In NestJS we can use Pipes for validation.

## Pipes

**Rule# 2:** Validation logic should be delegated to a separate entity known as pipe.

![Controller using Service and Pipes](./assets/images/javascript/nestjs__controller-using-service-and-pipes.avif)

Controller using Service and Pipes

In NestJS pipes are mainly used for transformation and validation. Let’s create a smart pipe. It not only validates input to be numeric, but also allows input containing commas. So while values like “abc” is not allowed, Pipe will accept “1,000” and strip commas from input before passing it to controller.  
_/smart/convert/12_ is allowed  
_/smart/convert/1,000_ is allowed, 1,000 will be treated as 1000  
_/smart/convert/abc_ is not allowed, raise 422 (UnprocessableEntityException)

```js
import {
  ArgumentMetadata,
  Injectable,
  PipeTransform,
  UnprocessableEntityException,
} from "@nestjs/common"

@Injectable()
export class CommaPipe implements PipeTransform {
  transform(value: any, metadata: ArgumentMetadata) {
    /* remove comma from input */
    var output = value.replaceAll(",", "")
    /* If input is Not a Number, raise 422 error  */
    if (isNaN(output)) {
      throw new UnprocessableEntityException(
        ["Non numeric input"],
        "Incorrect Parameter"
      )
    }
    return output
  }
}
```

And updated controller (using Pipe) is:

```js
import { Controller, Get, Param } from '@nestjs/common';
import { ConverterService } from './converter.service';
import { CommaPipe } from './comma.pipe';

@Controller('smart')
export class SmartController {
  constructor(private readonly converterService: ConverterService) {}
  /*
    We have used CommaPipe to validate "inr" path parameter
  */
  @Get('/convert/:inr')
  convert(@Param('inr', new CommaPipe()) inr: number): number {
    return this.converterService.convert(inr);
  }
}
```

> Lesson learnt so far: Delegate business logic to service and validation logic to pipes.

## Interceptors

**Rule# 3:** Response transformation should be delegated to a separate entity known as interceptor.

![NestJS Controller using Service and Pipes and Interceptor](./assets/images/javascript/nestjs__controller-using-service-and-pipes-and-interceptor.avif)

Controller using Service and Pipes and Interceptor

So far so good. But What if i want output to be in more presentable/readable form ? I want output to be formatted from **2400000** to **2,400,000** so as to offer readability to user. How can i do this ?
The answer is interceptors. Interceptors.

> Interceptors are used for applying custom logic and transforming response.

```js
import {
  CallHandler,
  ExecutionContext,
  Injectable,
  NestInterceptor,
  UnprocessableEntityException,
} from "@nestjs/common"
import { Observable } from "rxjs"
import { map } from "rxjs/operators"

@Injectable()
export class CommaInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    const request = context.switchToHttp().getRequest()
    return next.handle().pipe(
      map((data) => {
        /* adding comma every 3 digits */
        data = data.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",")
        return data
      })
    )
  }
}
```

Controller:

```js
import { Controller, Get, Param, UseInterceptors } from '@nestjs/common';
import { ConverterService } from './converter.service';
import { CommaPipe } from './comma.pipe';
import { CommaInterceptor } from './comma.interceptor';

@Controller('intercept')
export class InterceptController {
  constructor(private readonly converterService: ConverterService) {}

  @Get('/convert/:inr')
  /* Interceptor */
  @UseInterceptors(CommaInterceptor)
  /* Pipe for Param */
  convert(@Param('inr', new CommaPipe()) inr: number): number {
    return this.converterService.convert(inr);
  }
}
```

## Repository

**Rule# 4:** Data Layer should be isolated. Data access and manipulation logic should be delegated to a separate entity known as Repository.

![Controller using Service and Pipes and Interceptor and Repository](./assets/images/javascript/nestjs__controller-using-service-and-pipes-and-interceptor-and-repository.avif)

Controller using Service and Pipes and Interceptor and Repository

Connecting NestJs App to MongoDb or MYSQL or accessing external data via APIs is a vast topic. I will publish another tutorial for the same.
NestJs provides Middlewares and Guards as well. A Complete NestJS App using all nuts and bolts is explained below:

![NestJS App using Controllers, Services ,Pipes, Guards, Middlewares, Interceptors and Repository](./assets/images/javascript/nestjs__architecture.avif)

NestJS App using Controllers, Services ,Pipes, Guards, Middlewares, Interceptors and Repository

I suggest all readers to read the concept of providers from [official documentation of NestJs](https://docs.nestjs.com/first-steps).

Please read about [NestJS modules](https://docs.nestjs.com/modules) and refer to [app.module.ts](https://github.com/mansha99/nestjs-arch/blob/master/src/app.module.ts) file from repository. Source code may be downloaded from [this](https://github.com/mansha99/nestjs-arch/tree/master) repo.
Feel free to connect if you have any doubt, query or discussion.
Happy Coding.
