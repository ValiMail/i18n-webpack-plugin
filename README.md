<div align="center">
  <!-- replace with accurate logo e.g from https://worldvectorlogo.com/ -->
  <a href="https://github.com/webpack/webpack">
    <img width="200" height="200" vspace="" hspace="25"
      src="https://cdn.rawgit.com/webpack/media/e7485eb2/logo/icon.svg">
  </a>
  <h1>i18n Plugin</h1>
  <p>i18n (localization) plugin for Webpack.<p>
</div>

<h2 align="center">Install</h2>

npm
```bash
npm i -D @matthewbschneider/i18n-webpack-plugin
```
yarn
```bash
yarn add -D @matthewbschneider/i18n-webpack-plugin
```

<h2 align="center">Usage</h2>

This plugin creates bundles with translations baked in. So you can serve the translated bundle to your clients.
Example:
```
console.log(__("Hello World"));
console.log(__("Missing Text"));
```
```
var path = require("path");
var I18nPlugin = require("@matthewbschneider/i18n-webpack-plugin");
var languages = {
	"en": null,
	"de": require("./de.json")
};
module.exports = Object.keys(languages).map(function(language) {
	return {
		name: language,
		// mode: "development || "production",
		entry: "./example",
		output: {
			path: path.join(__dirname, "dist"),
			filename: language + ".output.js"
		},
		plugins: [
			new I18nPlugin(
				languages[language]
			)
		]
	};
});
```

```
// de.json
{
	"Hello World": "Hallo Welt"
}
```
current [example](https://github.com/zainulbr/i18n-webpack-plugin/tree/master/example). 
original [example](https://github.com/webpack/webpack/tree/v4.0.0/examples/i18n) from un maintenance repo 
<h2 align="center">Options</h2>

```
plugins: [
  ...
  new I18nPlugin(languageConfig, optionsObj)
],
```
 - `optionsObj.functionName`: the default value is `__`, you can change it to other function name.
 - `optionsObj.failOnMissing`: the default value is `false`, which will show a warning message, if the mapping text cannot be found. If set to `true`, the message will be an error message.
 - `optionsObj.hideMessage`: the default value is `false`, which will show the warning/error message. If set to `true`, the message will be hidden.
 - `optionsObj.nested`: the default value is `false`. If set to `true`, the keys in `languageConfig` can be nested. This option is interpreted only if `languageConfig` isn't a function.
