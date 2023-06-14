This repository owns every workflow I reuse too much.

Some are for Obsidian Plugins, other is more general.

## Obsidian Plugins

| Key         | Context | Type    | required | Description                 | default                                                                                                                        |
| ----------- | ------- | ------- | -------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| GH_TOKEN    | secrets | string  | true     | Your github token           | `secrets.GITHUB_TOKEN`                                                                                                         |
| PLUGIN_NAME | inputs  | string  | true     | You plugin ID (in manifest) |                                                                                                                                |
| STYLE       | inputs  | boolean | false    | If you use `styles.css`     | false                                                                                                                          |
| BETA        | inputs  | boolean | false    | false                       | Publish a beta release (without needing a beta version first). It just change the changelog used to generate the release note. |



As it uses some package for the building, you need to use [`obsidian-cli`](https://www.npmjs.com/package/obsidian-plugin-cli) to run it.

After bumping version, the plugin will be released on the release page.

You default `package.json` must look like this:
```json
{
    ...
    "scripts": {
        "build": "obsidian-plugin build [ENTRYPOINT]",
        "bump": "commit-and-tag-version"
    },
    "commit-and-tag-version": {
	    "t": ""
    },
    "devDependencies": {
        "obsidian-plugin-cli": "latest",
        "commit-and-tag-version": "^11.0.0"
    }
}
```

> **Note**  
> You don't need to have the "BETA" set to true to release a beta version if the version released contains the `-` character. 

### Bump 

Bump the version of the plugin based on the manifest.json file. It will use the `commit-and-tag-version` npm package to bump the version and create a tag. 

| Key          | Context | Type    | Required | Description                                    | Default              |
| ------------ | ------- | ------- | -------- | ---------------------------------------------- | -------------------- |
| PLUGIN_NAME  | inputs  | string  | true     | The name of your plugin                        | /                    |
| STYLE        | inputs  | boolean | false    | If you have a style.css in your plugin         | false                |
| BRANCH       | inputs  | string  | false    | The branch where the version push will be done | master               |
| GH_TOKEN     | secrets | string  | true     | The github token to made the push version      | secrets.GITHUB_TOKEN |
| AUTHOR_EMAIL | secrets | string  | false    | The author of the push commit                  | (see template) `github` |

### Obsidian plugin publish

On tags, release the plugin on the release page.

## Add labels

Add labels to an issue based on the name (lowercase) of the issue

## Auto assign

Automatically assign issue/PR to the owner of the repository

---

# ISSUE TEMPLATE

## Obsidian

ISSUE_TEMPLATE to easily create an issue for an Obsidian plugin. It will ask you the name of the plugin and the version of Obsidian you are using, also the parameters...

