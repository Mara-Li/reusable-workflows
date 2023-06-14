This repository owns every workflow I reuse too much.

Some are for Obsidian Plugins, other is more general.

## Obsidian Plugins

-> [Release & bump](./template/obsidian/release.yml)

Release obsidian plugin based on a tag version or a manual trigger.
The manual trigger with `bump` allow to bump the version. You can set the `beta` input to `true` to release a beta version.

### Release

On tags, release the plugin on the release page. You can also use a manual trigger to publish the plugin, without needing to bump the version.


| Key           | Context | Type    | required | Description                 | default                                                                                                                        |
| ------------- | ------- | ------- | -------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `GH_TOKEN`    | secrets | string  | true     | Your github token           | `secrets.GITHUB_TOKEN`                                                                                                         |
| `PLUGIN_NAME` | inputs  | string  | true     | You plugin ID (in manifest) |                                                                                                                                |
| `STYLE`       | inputs  | boolean | false    | If you use `styles.css`     | false                                                                                                                          |
| `BETA`        | inputs  | boolean | false    | false                       | Publish a beta release (without needing a beta version first). It just change the changelog used to generate the release note. |

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

Bump the version of the plugin based on the `manifest.json` file. It will use the [`commit-and-tag-version`](https://www.npmjs.com/package/commit-and-tag-version) npm package to bump the version and create a tag.

| Key          | Context | Type    | Required | Description                                    | Default                                                       |
| ------------ | ------- | ------- | -------- | ---------------------------------------------- | ------------------------------------------------------------- |
| `PLUGIN_NAME`  | inputs  | string  | true     | The name of your plugin                        | /                                                             |
| `STYLE`        | inputs  | boolean | false    | If you have a style.css in your plugin         | `false`                                                       |
| `BRANCH`       | inputs  | string  | false    | The branch where the version push will be done | `master`                                                      |
| `BETA`         | inputs  | string  | false    | If you want to publish a beta release          | `false`                                                       |
| `GH_TOKEN`     | secrets | string  | true     | The github token to made the push version      | `secrets.GITHUB_TOKEN`                                        |
| `AUTHOR_EMAIL` | secrets | string  | false    | The author of the push commit                  | (see template) `github-actions[bot]@users.noreply.github.com` |
| `AUTHOR_NAME`  | secrets | inputs  | false    | The mail author of the push commit             | (see template) `github-actions[bot]`                          |

Set `BETA` to `true` to publish a beta version. It will:
- Update the `manifest-beta.json` file
- Use the `CHANGELOG-beta.md` file to generate the release note

> **Note**  
> To use the `beta` option, you need to update your `package.json` and add this [script](https://github.com/Lisandra-dev/create-obsidian-plugin/blob/master/src/templates/commit-and-tag-version.js.ejs). 
> Don't forget to remove the `.ejs` extension.

Update your `package.json` as follow:
```json
    //...
    "scripts": {
		"bump": "node commit-and-tag-version.js"
        //...
    },
```


## Add labels

Add labels to an issue based on the name (lowercase) of the issue

## Auto assign

Automatically assign issue/PR to the owner of the repository

---

# ISSUE TEMPLATE

## Obsidian

ISSUE_TEMPLATE to easily create an issue for an Obsidian plugin. It will ask you the name of the plugin and the version of Obsidian you are using, also the parameters...
