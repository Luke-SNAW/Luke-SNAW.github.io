---
id: 2ijeu1j04o0qzmy7hzk1tlb
title: TypeScript
desc: ''
updated: 1652057957402
created: 1652057928334
---
- [Differences Between TypeScript Type vs Interface](https://www.educba.com/typescript-type-vs-interface/)
- [Stop SHOUTING = 'shouting'](https://swizec.com/blog/stop-shouting-shouting/)
- [Typing Component Props | React TypeScript Cheatsheets](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/basic_type_example/#basic-prop-types-examples)
- [TypeScript Generics: What’s with the Angle Brackets <>?](https://javascript.plainenglish.io/typescript-generics-whats-with-the-angle-brackets-4e242c567269)
- [Covariance and Contravariance in TypeScript](https://dmitripavlutin.com/typescript-covariance-contravariance/)
- [A Simple Explanation of Function Overloading in TypeScript](https://dmitripavlutin.com/typescript-function-overloading/)
- [TypeScript Features to Avoid](https://www.executeprogram.com/blog/typescript-features-to-avoid)
- [The Shocking Secret About Static Types](https://medium.com/javascript-scene/the-shocking-secret-about-static-types-514d39bf30a3)
- [Index Signatures in TypeScript](https://dmitripavlutin.com/typescript-index-signatures/)
  ```typescript
  type SpecificSalary = Record<'yearlySalary'|'yearlyBonus', number>
  interface StringByString {
    [key: string]: string | undefined;
  }
  const object: StringByString = {};
  ```
  
- [3 Useful TypeScript Patterns to Keep in Your Back Pocket](https://spin.atomicobject.com/2021/05/11/3-useful-typescript-patterns/)
  ```typescript
  type Names = "Bob" | "Bill" | "Ben";
  type JobTitles = "Welder" | "Carpenter" | "Plumber";

  const JobAssignments: { [Key in Names]: JobTitles } = {
    Bob: "Welder",
    Bill: "Carpenter",
    Ben: "Plumber"
  };
  ```