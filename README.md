# designs

@fohte's personal design workspace for Claude Design canvases and shared design systems, edited with the [baoyu-design](https://github.com/JimLiu/baoyu-design) skills.

## Install the skills

The skill files are not committed, because their upstream NOTICE grants no license for the parts adapted from Anthropic's material. Install them into this repository from its root:

```sh
DO_NOT_TRACK=1 npx skills@1.7.6 add JimLiu/baoyu-design --skill claude-design-system claude-design --agent claude-code -y
```

`skills-lock.json` records the installed versions, and this command rewrites it.
