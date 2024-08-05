# eslint-config-no-autofix

An ESLint config that imports [`eslint-plugin-no-autofix`](https://github.com/aladdin-add/eslint-plugin/tree/master/packages/no-autofix), without turning on any other rules or settings. Specifically, it looks like this:

```js
module.exports = {
  plugins: ["no-autofix"],
};
```

## Why?

This plugin [does not yet support the ESLint flat config](https://github.com/aladdin-add/eslint-plugin/issues/92). We can work around this by using the [`FlatCompat`](https://eslint.org/docs/latest/use/configure/migration-guide#using-eslintrc-configs-in-flat-config) utility. But that can only be used on configs, not on plugins. Thus, we need to arbitrarily compose a config that contains only the plugin.

## Usage

```ts
import tseslint from "typescript-eslint";

const compat = new FlatCompat({
  baseDirectory: import.meta.dirname,
});

export default tseslint.config(
  ...compat.extends("eslint-config-no-autofix"),
  // Add your other configuration here.
);
```

(Using the [`tseslint.config`](https://typescript-eslint.io/packages/typescript-eslint#config) helper function is not technically necessary, but composing flat configs with the helper function is considered best practice.)
