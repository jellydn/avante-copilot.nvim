<h1 align="center">Welcome to avante-copilot.nvim - a fork of avante.nvim 👋</h1>
<p>
  Bring back the Copilot provider for the open-source world :)
</p>

> [!IMPORTANT]
>
> If your neovim doesn't use LuaJIT, then change `build` to `make lua51`. By default running make will install luajit.
> Avante.nvim will now requires cargo to build tiktoken_core from source.

## Usages

Simple usage like this, please refer to the available options in the [yetone/avante.nvim](https://github.com/yetone/avante.nvim)

```lua
{
  "jellydn/avante-copilot.nvim",
  event = "VeryLazy",
  build = "powershell -ExecutionPolicy Bypass -File Build-LuaTiktoken.ps1", -- This is Optional, only if you want to use tiktoken_core to calculate tokens count
  -- rest of the config
}
```

My working config with lazy.nvim:

```lua
return {
{
    "jellydn/avante-copilot.nvim",
    event = "VeryLazy",
    build = "make",
    opts = {
      provider = "copilot", -- You can then change this provider here
      -- provider = "claude",
      mappings = {
        ask = "<leader>ra",
        edit = "<leader>re",
        refresh = "<leader>rr",
      },
    },
    dependencies = {
      "nvim-lua/plenary.nvim",
      "MunifTanjim/nui.nvim",
    },
    config = function(_, options)
      require("avante").setup(options)

      local wk = require("which-key")
      wk.add({
        { "<leader>ra", desc = "Ask AI" },
        { "<leader>re", desc = "Edit selected" },
        { "<leader>rr", desc = "Refresh AI" },
      })
    end,
  },
  {
    "MeanderingProgrammer/render-markdown.nvim",
    optional = true,
    opts = {
      file_types = { "markdown", "Avante" },
    },
    ft = { "markdown", "Avante" },
  },
  {
    "folke/which-key.nvim",
    optional = true,
    opts = {
      spec = {
        { "<leader>r", group = "Refactor/AI" },
      },
    },
  },
}
```

[![Copilot](https://i.gyazo.com/abab6b0aa05cf559d136d2f5180ed2fa.gif)](https://gyazo.com/abab6b0aa05cf559d136d2f5180ed2fa)

## Show your support

Give a ⭐️ if this project helped you!
