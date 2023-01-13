# 2023-01-13

## Support for running commands via just

We've previously used [make](https://www.gnu.org/software/make/) for easily running some playbook commands (e.g. `make roles` which triggers `ansible-galaxy`, see [Makefile](Makefile)).
Our `Makefile` is still around and you can still run these commands.

In addition, we've added support for running commands via [just](https://github.com/casey/just) - a more modern command-runner alternative to `make`. Instead of `make roles`, you can now run `just roles` to accomplish the same.

Our [justfile](justfile) already defines some additional helpful **shortcut** commands that weren't part of our `Makefile`. Here are some examples:

- `just install-all` to trigger the much longer `ansible-playbook -i inventory/hosts setup.yml --tags=install-all,start` command
- `just install-all --ask-vault-pass` - commands also support additional arguments (`--ask-vault-pass` will be appended to the above installation command)
- `just run-tags install-gitea-backup,start` - to run specific playbook tags
- `just start-all` - (re-)starts all services
- `just stop-group postgres` - to stop only the Postgres service

Additional helpful commands and shortcuts may be defined in the future.

This is all completely optional. If you find it difficult to [install `just`](https://github.com/casey/just#installation) or don't find any of this convenient, feel free to run all commands manually.


# 2022-12-16

Initial release
