This repository owns every workflow I reuse too much.

Some are for Obsidian Plugins, other is more general.

## Obsidian Plugins

| Key         | Context | Type    | required | Description                 | default                |
|-------------|---------|---------|----------|-----------------------------|------------------------|
| GH_TOKEN    | secrets | string  | true     | Your github token           | `secrets.GITHUB_TOKEN` |
| PLUGIN_NAME | inputs  | string  | true     | You plugin ID (in manifest) |                        |
| STYLE       | inputs  | boolean | false    | If you use `styles.css`     | false                  |

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
### Bump 

Bump the version of the plugin based on the manifest.json file. It will use the `commit-and-tag-version` npm package to bump the version and create a tag. 

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

