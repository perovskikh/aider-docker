# Launch Aider in Docker with Ansible Configuration

Vibe coding with [Aider](https://github.com/Aider-AI/aider) and local [Ollama](https://github.com/ollama/ollama) models. This project uses Ansible to set up configuration variables (project_dir, model_name, ollama_api) in a secure/var directory.

### Configuration

This project is configured using Ansible. The `make gen` command runs an Ansible playbook that prompts for the following values or uses defaults:

- Project directory
- Model name
- Ollama API URL
- Conventions (project-specific coding conventions)

These variables are stored in a secure/var directory and can also be overridden by setting environment variables.

### Launch Aider

```bash
git clone https://github.com/HardAndHeavy/aider-docker
cd aider-docker
make gen # This will prompt for default values and set up configuration files (config/.aider.conf.yml, config/.env)
```

The `gen` target uses the following Ansible variables:

- conventions: "{{ lookup('file', '../secure/var/conventions', errors='ignore') | default('The project is being developed in python', true) }}"
- model_name: "{{ lookup('file', '../secure/var/model_name', errors='ignore') | default('qwen2.5-coder:32b-instruct-q4_K_M', true) }}"
- ollama_api: "{{ lookup('file', '../secure/var/ollama_api', errors='ignore') | default('http://host.docker.internal:11434', true) }}"

Then you can launch Aider with:

```bash
make run # This runs the Ansible playbook to set up the environment from secure/var and then starts Aider with docker
```

To manually control which variables are used, create a `secure/var` directory (if not already present) containing configuration files or override existing ones.

### Additional Information

The project uses Ansible templates for:
- config/.aider.conf.yml: Contains Aider settings from secure/var
- config/.env: Environment file with variable overrides

You can view the full template structure in `ansible/templates`.
