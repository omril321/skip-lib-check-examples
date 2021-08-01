# skipLibCheck Example 3 - Valid types are never ignored

In this example, you can see that `tsc` will always check valid types, even if they are imported from an invalid file.

Without `skipLibCheck`, `tsc` will throw two errors: one for an invalid type declaration, and one for misusing a function declared in the same file:  

```bash
> npx tsc --project . && echo 'success!'

index.ts:4:10 - error TS2345: Argument of type 'string' is not assignable to parameter of type 'number'.

4 doubleIt('not a number');
           ~~~~~~~~~~~~~~

some-file.d.ts:1:28 - error TS2304: Cannot find name 'NON_EXISTING_TYPE'.

1 export type INVALID_TYPE = NON_EXISTING_TYPE;
                             ~~~~~~~~~~~~~~~~~


Found 2 errors.
```

When compiling with `skipLibCheck`, the invalid type will be ignored - as we've seen on previous examples. Additionally, we see that we still get an error for unexpected parameter type for function `doubleIt` (even though the function was declared in an invalid declaration file):

```bash
> npx tsc  --project . --skipLibCheck && echo 'success!'

index.ts:4:10 - error TS2345: Argument of type 'string' is not assignable to parameter of type 'number'.

4 doubleIt('not a number');
           ~~~~~~~~~~~~~~


Found 1 error.
```

This example shows that with `skipLibCheck` the declaration files are not being skipped completely.
