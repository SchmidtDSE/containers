
# Test LLM clients in a container



This docker container has preinstalled versions of several LLM cli-tools.  Running in a container can be a convenient way to control the limit the scope of what the LLM can access on your machine without having to trust the developers.  


Below we also document how to configure these to access various models, including free models and open source models.


The following interfaces are preinstalled:

- claude code: https://github.com/anthropics/claude-code
- copilot cli: https://github.com/github/copilot-cli
- codex-cli: https://github.com/openai/codex
- cline-cli: https://github.com/cline/cline/tree/main/cli

## copilot-cli

Because copilot is free with a GitHub account (and 'premium' models are free to .edu accounts), it is a good starting point:


```
docker run --rm -ti ghcr.io/schmidtdse/llm copilot
```

Copilot can also be configured to work with various local / open models, including [the models hosted by NRP](https://nrp.ai/documentation/userdocs/ai/llm-managed/)

```
Add configuration here by volume linking a `.copilot/config.toml`  file
```

## opencode.ai

```
docker run --rm -ti -v $(pwd)/opencode.json:/workdir/.opencode.json -e NRP_API_KEY=$NRP_API_KEY ghcr.io/schmidtdse/llm opencode
```


## cline-cli

Cline is an open-source vscode extension that also has a command-line tool.  Though development has focused on Anthropic's models, cline is the only one on this list that is unaffiliated with any specific AI lab and has excellent support for a broad base of models. 


## claude

```
docker run --rm -ti -e ANTHROPIC_BASE_URL=https://ellm.nrp-nautilus.io -e ANTHROPIC_MODEL='glm-4.6' -e ANTHROPIC_AUTH_TOKEN=$ANTHROPIC_AUTH_TOKEN ghcr.io/schmidtdse/llm claude
```


