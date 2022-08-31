# NVIM-DAP-PROJECTS

A very simple plugin which implements "per-project" nvim-dap debugger adapters
and configurations. 

This plugin allows source code maintainers to place a `nvim-dap` configuration
file in a configurable location in their repository. When this plugin discovers
the file it will only display the debugger configurations within this project 
local configuration. 

This should feel very similar to how `vscode` works. `vscode` does not display
all debuger configurations across all projects, but rather only displays the 
debugger configurations relevant for the open project. 

If this plugin does not find a local configuration file it simply performs no
action and `nvim-dap`'s global configuration file will be used to display debugger
configurations.

## Usage

Using plug or your favorite plugin manager:
```
...
    Plug 'ldelossa/nvim-dap-projects'
call plug#end()
lua require('nvim-dap-projects').search_project_config()
```

Install the plugin and then call it's `search_project_config` method at any point
after its install. 

By default the paths `./nvim-dap.lua`, `./.nvim-dap/nvim-dap.lua` and `.nvim/nvim-dap.lua` are searched
for.

You may modify this by changing or appending to the plugin's `config_paths` array
before calling `search_project_config`.

```
lua require('nvim-dap-projects').config_paths = {"./test/nvim-dap.lua"}
lua require('nvim-dap-projects').search_project_config()
```
Always provide the relative path to the actual config file, this allows you to
change the name of the config file if you'd like.

If the plugin discovers a `nvim-dap.lua` file then a calling to 'DapContinue' 
will only display the locally defined debug configurations.
