
## Collections

### [How can I use wildcards to `cp` a group of files with the AWS CLI?](https://stackoverflow.com/a/38834779/5163033)

```sh
aws s3 cp s3://data/ . --recursive --exclude "*" --include "2016-08*"
```

I'd like to point out the `--exclude "*"` isn't a typo. _If you don't add it, the include will match anything_.
