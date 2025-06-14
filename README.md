# Launch Aider in Docker with Ansible Configuration

Vibe coding with [Aider](https://github.com/Aider-AI/aider) and local [Ollama](https://github.com/ollama/ollama) models. This project uses Ansible to set up configuration files (config/.aider.conf.yml, config/.env) from templates.

### Configuration

The `make gen` command runs an Ansible playbook that prompts for or imports the following values:

- conventions: "{{ lookup('file', '../secure/var/conventions', errors='ignore') | default('Standard Conventions', true) }}"
- model_name: "{{ lookup('file', '../secure/var/model_name', errors='ignore') | default('qwen2.5-coder:32b-instruct-q4_K_M', true) }}"
- ollama_api: "{{ lookup('file', '../secure/var/ollama_api', errors='ignore') | default('http://host.docker.internal:11434', true) }}"

These variables are stored in a `secure/var` directory and can be overridden by setting environment variables.

### Launch Aider

```bash
git clone https://github.com/HardAndHeavy/aider-docker
cd aider-docker
make gen # This will prompt for default values or import existing ones from secure/var
```

Then you can launch Aider with:

```bash
make run # This runs the Ansible playbook to set up configuration and then starts Aider with docker
```

### Additional Information

The project uses Ansible templates in `ansible/templates` that generate:
- config/.aider.conf.yml: Contains Aider settings from secure/var
- config/.env: Environment file with variable overrides

You can manually control the values by creating a `secure/var` directory containing configuration files.
