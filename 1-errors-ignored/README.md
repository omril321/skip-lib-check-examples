# skipLibCheck Example 1 - Ignoring Errors

In this example, you can see that `tsc` ignores errors coming from invalid types or syntax errors.

When compiling without `skipLibCheck`:

```bash
> npx tsc --project . && echo 'success!'

some-file.d.ts:1:37 - error TS2339: Property 'invalid-prop' does not exist on type 'Number'.

1 export type INVALID_TYPE_1 = number['invalid-prop'];
                                      ~~~~~~~~~~~~~~

some-file.d.ts:3:30 - error TS2304: Cannot find name 'NON_EXISTING_TYPE'.

3 export type INVALID_TYPE_2 = NON_EXISTING_TYPE;
                               ~~~~~~~~~~~~~~~~~

some-file.d.ts:5:1 - error TS1036: Statements are not allowed in ambient contexts.

5 oh_no_unexpected_string;
  ~~~~~~~~~~~~~~~~~~~~~~~

some-file.d.ts:5:1 - error TS2304: Cannot find name 'oh_no_unexpected_string'.

5 oh_no_unexpected_string;
  ~~~~~~~~~~~~~~~~~~~~~~~


Found 4 errors.
```

When compiling with `skipLibCheck`, the syntax and type errors are being ignored:

```bash
> npx tsc  --project . --skipLibCheck && echo 'success!'

success!
```
