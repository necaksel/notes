# OPS meeting 11.12.24
11.12.2024

This is how Stian locks down a machine behind tailscale
https://neconcoimmunity.atlassian.net/browse/OPS-512

Stephane: "I am not a developer, but I am learning"

Stian: "it is up to you to figure out how to move forward with this"
Software development is run by individuals and you lead initiatives
yourself.
Stian said this earlier today you can do the uv ansible script, 
that is up to you.

self-hosted uses any self hosted runner that is available.
So jobs can execute on these runners already.

You have to install uv.
Could we install things with nix?

isort, flake8, black replace with ruff.
make format will be the same.

Have engineering establish a pawed path, the golden road that you
support well. You can do your own thing. But then you get less support.

Collaborate with [[Erlend Fauchaldon]] on a cookiecutter update.
Get uv working well in indit, then use that as an example.
[[Moritz von Stetten]] suggests using ruff for all formatting. I like that suggestion
Those two could form the basis of a great overhaul of the cookiecutter update.

Got an intro to [[ansible-server-automation]] and [[Ansible]] from [[Stian Lagstad]].
Declarative (nix, terraform) is nicer than imperative (ansible).
Relevant for [[uv in indit]]

Path of least resistance for uv is to add it alongside the pip env var in the pip task.


