lsof -i:8021

kill -9 70584(PID)



```ja
Software Installation
	•	Install node.js. Recommended to install the LTS version. After the installation is complete, run node -v in the terminal. If the version information can be output normally, the installation is successful
￼
	•	Install vscode, just install it directly
VS Code Plugin installation
	•	path-intellisense →  Path completion prompt, support path alias
	•	vetur  → Support vue code hint
	•	eslint → Support real-time check JS
	•	prettier → Format code automatically when saving
	•	vscode-icons → Mark different icons for files (optional)
Installation method, open VS Code click the extension button on the left and enter the plug-in to be installed
￼
VS Code Plugin configuration
	•	Configuration method, click the button in the lower left corner of the window and select Settings
￼
	•	Enter settings and click Edit in settings.json
￼
	•	Use the following configuration to overwrite the settings.json file
{
  "workbench.startupEditor": "newUntitledFile",
  "search.exclude": {
    "**/node_modules": true,
    "**/bower_components": true,
    "**/dist": true,
    "**/target": true
  },
  "editor.cursorStyle": "block",
  "editor.fontFamily": "Fira Code",
  "editor.fontLigatures": true,
  "editor.fontSize": 14,
  "editor.lineHeight": 24,
  "editor.lineNumbers": "on",
  "editor.renderIndentGuides": false,
  "editor.rulers": [120],
  "editor.quickSuggestions": {
    "other": true,
    "comments": false,
    "strings": true
  },
  "editor.renderWhitespace": "boundary",
  "editor.cursorBlinking": "smooth",
  "editor.minimap.enabled": true,
  "editor.minimap.renderCharacters": false,
  "editor.codeLens": true,
  "editor.snippetSuggestions": "top",
  "window.title": "${dirty}${activeEditorMedium}${separator}${rootName}",
  "workbench.colorTheme": "Default Dark+",
  "workbench.iconTheme": "vscode-icons",
  "explorer.confirmDragAndDrop": false,
  "editor.suggestSelection": "first",
  "files.associations": {
    "*.vue": "vue"
  },
  "emmet.syntaxProfiles": {
    "javascript": "jsx",
    "vue": "html",
    "vue-html": "html"
  },
  "editor.codeActionsOnSave": {
    "source.fixAll.tslint": true,
    "source.fixAll.eslint": true
  },
  "json.maxItemsComputed": 10000,
  "vsicons.dontShowNewVersionMessage": true,
  "files.autoSave": "off",
  "search.followSymlinks": false,
  "git.autorefresh": false,
  "workbench.editor.showTabs": false,
  "search.searchOnType": false,
  "path-intellisense.mappings": {
    "@": "${workspaceRoot}/src"
  },
  "editor.formatOnSave": true,
  "liveServer.settings.donotShowInfoMsg": true,
  "notebook.kernelProviderAssociations": [],
  "eslint.alwaysShowStatus": true,
  "prettier.configPath": ".prettierrc.json",
  "prettier.ignorePath": ".prettierignore",
  "vetur.format.defaultFormatter.js": "none",
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}

 Download project
	•	git clone -b wos_master https://bitbucket-eng-chn-sjc1.cisco.com/bitbucket/scm/cctgcloud/cloudtools-gfc.git
	•	Navigate to the wos-portal directory and open in VS Code 
Install project dependencies
	•	Right-click in the left window to open the terminal
￼

	•	Run npm install to install the dependent packages of the project. After the dependent packages are installed, run npm run dev to start the project.
	•	You can view the configured commands in package.json

```

