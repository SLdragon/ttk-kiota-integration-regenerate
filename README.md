# TTK-Kiota Integration - Regenerate support

This sample proposes new project structure uses kiota generated `{service-name}-apiplugin.json` and `{service-name}-openapi.yml` files in the root of `appPackage` directly, without needing to copy them to different folders and change names.

## Current Missing Parts
- Scaffolding structure changes (TTK)
- Adaptive card re-generation (TTK, Kiota)

## TTK Changes
- When scaffolding project from Kiota, update `declarativeAgent.json` file to point to Kiota generated files `{service-name}-apiplugin.json`, `{service-name}-openapi.yml`
- Copy `.kiota` folder to project root
- Add a new command/Update current command to update/generate adaptive card/teamsapp.yaml

## Kiota Changes
- After user clicks re-generation, Kiota needs to call TTK to update/generate adaptive cards, update teamsapp.yaml file (this is neccessary for API with auth)
- If Kiota can generate adaptive card in the future, TTK will only handle teamsapp.yaml file update

## Draft Command for Re-generation

Re-use original `fx-extension.createprojectfromkiota`, and added a type propety, which accept `regenerate` and `create`

```javascript
const result = await vscode.commands.executeCommand(
  'fx-extension.createprojectfromkiota',
  [
    'C:/tmp/openapi.yaml',
    'C:/tmp/ai-plugin.json',
    context,
    type: "regenerate|create"
  ]
);
```
