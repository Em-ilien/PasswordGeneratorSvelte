# PasswordGeneratorSvelte

## Description

PasswordGeneratorSvelte is a Svelte component that allows for generating random passwords with options to choose the length and to enable or disable lowercase letters, uppercase letters, numbers, and symbols.

## Installation

To install the library, use npm:

```bash
npm install password-generator-svelte
```

## Usage

Here is an example of using PasswordGeneratorSvelte:

```svelte
<script>
	import { PasswordGeneratorSvelte } from 'password-generator-svelte';
</script>

<div>
	<PasswordGeneratorSvelte />
</div>
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Author

Emilien Cosson

## Contribution

Any contributions are welcome! Please follow these steps to contribute:

1. Open an issue on GitHub to discuss your changes.
2. Make your changes and submit a Pull Request (PR).
3. Commits should follow the syntax below:

```
<type>(<scope>): <subject>

<description>

<footer>
```

- **Type** defines the type of commit (build, ci, docs, feat, fix, perf, refactor, style, test).
- **Scope** defines which part of the library/application is affected (optional).
- **Subject** is a brief description of the changes, using the imperative mood and without a capital letter or period.
- **Description** provides a more detailed explanation of the motivations behind the change (following the same rules as the Subject).
- **Footer** contains important changes (Breaking Changes) and references to GitHub/GitLab issues or others.

## Developing

Start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

Everything inside `src/lib` is part of the library, everything inside `src/routes` can be used to test or preview the component.

## Building

To build the library:

```bash
npm run package
```

To create a production version of the showcase app:

```bash
npm run build
```

To preview the production build with `npm run preview`.

> To deploy the app, install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.

## Publishing

```bash
npm publish
```
