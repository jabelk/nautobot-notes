# nautobot-notes


## Docker Compose start up

https://github.com/nautobot/nautobot-docker-compose?tab=readme-ov-file#cleanup-everything-and-start-from-scratch

Build and Start Nautobot should have disclaimer that if it is your first time doing this to scroll down to the Getting Started. I just assumed you should start putting in commands after installing poetry. I figured there was something wrong with config file after seeing output, but could have been avoided with a table of contents at top or more context in the flow. 

The "How to use this repo" would also be a good place to give guidance on the user flow. 

https://github.com/nautobot/nautobot-docker-compose?tab=readme-ov-file#getting-started



```

#12 13.86 In order to avoid a breaking change and make your automation forward-compatible, please install poetry-plugin-export explicitly. See https://python-poetry.org/docs/plugins/#using-plugins for details on how to install a plugin.
#12 13.86 To disable this warning run 'poetry config warnings.export false'.
#12 DONE 14.3s

#13 [nautobot builder 6/8] COPY ../jobs /opt/nautobot/jobs
#13 DONE 0.0s

#14 [nautobot builder 7/8] COPY ../config/nautobot_config.py /opt/nautobot/nautobot_config.py
#14 DONE 0.0s

#15 [nautobot builder 8/8] WORKDIR /source
#15 DONE 0.0s

#16 [nautobot nautobot 1/5] COPY --from=builder /tmp/dist /tmp/dist
#16 DONE 0.0s

#17 [nautobot nautobot 2/5] COPY --from=builder /opt/nautobot /opt/nautobot
#17 DONE 0.0s

#18 [nautobot nautobot 3/5] COPY --from=builder /usr/local/lib/python3.8/site-packages /usr/local/lib/python3.8/site-packages
#18 DONE 5.3s

#19 [nautobot nautobot 4/5] COPY --from=builder /usr/local/bin /usr/local/bin
#19 DONE 0.1s

#20 [nautobot nautobot 5/5] RUN pyuwsgi --cflags | sed 's/ /\n/g' | grep -e "^-DUWSGI_SSL$"
#20 0.174 -DUWSGI_SSL
#20 DONE 0.2s

#21 [nautobot] exporting to image
#21 exporting layers
#21 exporting layers 1.8s done
#21 writing image sha256:49193f2d0d91b3e895489a8310786876127a79963d909642474caf81f9d612d2 done
#21 naming to docker.io/yourrepo/nautobot-docker-compose:local done
#21 DONE 1.8s

#22 [nautobot] resolving provenance for metadata file
#22 DONE 0.0s
(nautobot-docker-compose-py3.10) nautobot-docker-compose$ invoke start
Starting Nautobot in detached mode...
Running docker compose command "up --detach"
env file /Users/jabelk/dev/projects/nautobot-learn/docker-test/nautobot-docker-compose/environments/local.env not found: stat /Users/jabelk/dev/projects/nautobot-learn/docker-test/nautobot-docker-compose/environments/local.env: no such file or directory
(nautobot-docker-compose-py3.10) nautobot-docker-compose$ pwd
/Users/jabelk/dev/projects/nautobot-learn/docker-test/nautobot-docker-compose
(nautobot-docker-compose-py3.10) nautobot-docker-compose$
```


```
(nautobot-docker-compose-py3.10) nautobot-docker-compose$ poetry env info

Virtualenv
Python:         3.10.4
Implementation: CPython
Path:           /Users/jabelk/Library/Caches/pypoetry/virtualenvs/nautobot-docker-compose-gRtuJhB6-py3.10
Executable:     /Users/jabelk/Library/Caches/pypoetry/virtualenvs/nautobot-docker-compose-gRtuJhB6-py3.10/bin/python
Valid:          True

Base
Platform:   darwin
OS:         posix
Python:     3.10.4
Path:       /Users/jabelk/.pyenv/versions/3.10.4
Executable: /Users/jabelk/.pyenv/versions/3.10.4/bin/python3.10
(nautobot-docker-compose-py3.10) nautobot-docker-compose$
```



https://github.com/nautobot/nautobot-docker-compose?tab=readme-ov-file#create-super-user-via-environment

Add some additional verbiage around if you are unable to authenticate into the application and this is your first time using this, there is no default admin / admin user, even though it shows up in the creds file, you need to do this to authenticate. 



## Installing device onboarding app

https://github.com/nautobot/nautobot-docker-compose/blob/main/docs/plugins.md#adding-apps-using-pypi

Followed commands through `invoke stop start` and updated config file per example. localhost not coming back up.

noticed the recommendation here:
https://docs.nautobot.com/projects/core/en/stable/user-guide/administration/installation/app-install/#run-nautobot-server-post_upgrade
to use `nautobot-server post_upgrade` after installing an app which was not in the github markdown flow. 

Got the following error:

```
(nautobot-docker-compose-py3.10) nautobot-docker-compose$ nautobot-server post_upgrade
Traceback (most recent call last):
  File "/Users/jabelk/Library/Caches/pypoetry/virtualenvs/nautobot-docker-compose-gRtuJhB6-py3.10/bin/nautobot-server", line 8, in <module>
    sys.exit(main())
  File "/Users/jabelk/Library/Caches/pypoetry/virtualenvs/nautobot-docker-compose-gRtuJhB6-py3.10/lib/python3.10/site-packages/nautobot/core/cli/__init__.py", line 292, in main
    load_settings(args.config_path)
  File "/Users/jabelk/Library/Caches/pypoetry/virtualenvs/nautobot-docker-compose-gRtuJhB6-py3.10/lib/python3.10/site-packages/nautobot/core/cli/__init__.py", line 131, in load_settings
    raise FileNotFoundError(
FileNotFoundError: Configuration file not found at /Users/jabelk/.nautobot/nautobot_config.py - Please provide a valid --config-path path, or use 'nautobot-server init' to create a new configuration.
(nautobot-docker-compose-py3.10) nautobot-docker-compose$
```

I am thinking the no cache deleted out the config files that were there?

config is 

```

# Enable installed plugins. Add the name of each plugin to the list.
# PLUGINS = ["nautobot_example_plugin"]
PLUGINS = ["nautobot-device-onboarding"]

# Plugins configuration settings. These settings are used by various plugins that the user may have installed.
# Each key in the dictionary is the name of an installed plugin and its value is a dictionary of settings.
PLUGINS_CONFIG = {
    "nautobot-device-onboarding": {},
}
```

Tried updating config again and same result no database. 


## golden config

removed device onboarding app from config, tried installing golden config, similar error to device onboarding 

```
(nautobot-docker-compose-py3.10) nautobot-docker-compose$ nautobot-server post_upgrade
Traceback (most recent call last):
  File "/Users/jabelk/Library/Caches/pypoetry/virtualenvs/nautobot-docker-compose-gRtuJhB6-py3.10/bin/nautobot-server", line 8, in <module>
    sys.exit(main())
  File "/Users/jabelk/Library/Caches/pypoetry/virtualenvs/nautobot-docker-compose-gRtuJhB6-py3.10/lib/python3.10/site-packages/nautobot/core/cli/__init__.py", line 292, in main
    load_settings(args.config_path)
  File "/Users/jabelk/Library/Caches/pypoetry/virtualenvs/nautobot-docker-compose-gRtuJhB6-py3.10/lib/python3.10/site-packages/nautobot/core/cli/__init__.py", line 131, in load_settings
    raise FileNotFoundError(
FileNotFoundError: Configuration file not found at /Users/jabelk/.nautobot/nautobot_config.py - Please provide a valid --config-path path, or use 'nautobot-server init' to create a new configuration.
(nautobot-docker-compose-py3.10) nautobot-docker-compose$
```


```
(nautobot-docker-compose-py3.10) nautobot-docker-compose$ poetry add nautobot-golden-config
Using version ^2.1.2 for nautobot-golden-config

Updating dependencies
Resolving dependencies... (0.2s)

The current project's supported Python range (>=3.9,<3.13) is not compatible with some of the required packages Python requirement:
  - nautobot-golden-config requires Python <3.12,>=3.8, so it will not be satisfied for Python >=3.12,<3.13

Because no versions of nautobot-golden-config match >2.1.2,<3.0.0
 and nautobot-golden-config (2.1.2) requires Python <3.12,>=3.8, nautobot-golden-config is forbidden.
So, because nautobot-docker-compose depends on nautobot-golden-config (^2.1.2), version solving failed.

  • Check your dependencies Python requirement: The Python requirement can be specified via the `python` or `markers` properties

    For nautobot-golden-config, a possible solution would be to set the `python` property to ">=3.9,<3.12"

    https://python-poetry.org/docs/dependency-specification/#python-restricted-dependencies,
    https://python-poetry.org/docs/dependency-specification/#using-environment-markers
(nautobot-docker-compose-py3.10) nautobot-docker-compose$
```

It looks like you've encountered a dependency resolution issue while trying to add `nautobot-golden-config` to your project using Poetry. This issue arises because the `nautobot-golden-config` package specifies that it requires Python `<3.12,>=3.8`, and your project’s Python version constraint is `>=3.9,<3.13`. This leads to a conflict for future Python versions between `3.12` and `3.13`, which `nautobot-golden-config` does not support.

Here’s what you can do to resolve this:

1. **Adjust your project's Python constraint** to match the dependencies' constraints more closely. Since you are currently using Python 3.10.4, you can explicitly limit your project's Python version to `<3.12` to avoid conflicts with potential future versions. Modify your `pyproject.toml` file to reflect this:
   
   ```toml
   [tool.poetry.dependencies]
   python = "^3.10"
   ```

   This constraint ensures compatibility with current and minor future updates of Python 3.10 but excludes Python 3.12 and beyond, aligning with the requirements of `nautobot-golden-config`.

2. **Run `poetry update`** to apply the changes and resolve dependencies again.

If you anticipate needing to use Python versions higher than 3.11 in the future, you might want to contact the maintainers of `nautobot-golden-config` or watch for updates that expand compatibility to later Python versions. Adjusting your project’s Python version requirement in this way ensures you avoid version conflicts while maintaining the necessary flexibility for updates within your currently used Python version.


In your case, the error is not indicating a need for Python 3.12; rather, it's a compatibility issue caused by how your project's Python version constraints might intersect with the future. The `nautobot-golden-config` specifies that it requires a Python version that is greater than or equal to 3.8 but less than 3.12. This range is compatible with your current Python version, 3.10.4.

The conflict arises because your project's Python version is set to allow versions up to less than 3.13. This upper limit includes future versions of Python (3.12.x) which are not supported by `nautobot-golden-config` as per its current specification. The Poetry error message is a preventative warning indicating that if your Python version were to be updated to 3.12 or newer in the future, it would not be compatible with `nautobot-golden-config`.

**To resolve this, you should adjust your project’s Python version constraint to explicitly exclude Python 3.12 and newer versions**. Since you are using Python 3.10.4, setting your project's Python requirement in `pyproject.toml` to `^3.10` or `>=3.8,<3.12` ensures compatibility with your dependencies and avoids encompassing unsupported Python versions in the future:

```toml
[tool.poetry.dependencies]
python = ">=3.8,<3.12"
```

This setup tells Poetry that your project should be using a Python version that is at least 3.8 but less than 3.12, preventing future conflicts while still being compatible with your current environment.


The error message you're encountering suggests that the Python version constraint in your project's `pyproject.toml` file allows for Python versions up to less than 4.0, which might cause future compatibility issues with `nautobot`, which only supports up to Python 3.12. To resolve this, you need to adjust the Python version constraint in your `pyproject.toml` file to ensure it is compatible with all your dependencies.

In your `pyproject.toml`, you've set `python = "^3.10"` which implies compatibility with any Python 3.10.x version up to, but not including, Python 4.0. To match the requirement of `nautobot` and avoid potential future compatibility issues, you should change this line to restrict the Python version to less than 3.13. Here's how you can adjust your file:

```toml
[tool.poetry.dependencies]
python = ">=3.10,<3.13"
nautobot = "2.3.6"
nautobot-device-onboarding = "^4.1.0"
```

This change ensures that your project's Python environment will not upgrade to Python 3.13 or newer, which is currently unsupported by `nautobot`. After making this change, run `poetry update` again to resolve dependencies under the updated constraints. This should solve the version solving error and ensure that all your dependencies are compatible with the version of Python you are using.


Thanks for sharing your `pyproject.toml` content. To fix the dependency resolution issue with `nautobot-golden-config`, you'll need to adjust the Python version constraint specifically to match what `nautobot-golden-config` requires. Currently, your project allows Python versions from 3.10 up to, but not including, 3.13. However, `nautobot-golden-config` requires Python to be less than 3.12, which is causing the conflict.

You can modify your `pyproject.toml` as follows to align with the requirements of `nautobot-golden-config`:

```toml
[tool.poetry.dependencies]
python = ">=3.10,<3.12"  # Adjusted to upper limit <3.12 to match nautobot-golden-config requirements
nautobot = "2.3.6"
nautobot-device-onboarding = "^4.1.0"
nautobot-golden-config = "^2.1.2"
```

By changing the Python version to `">=3.10,<3.12"`, you ensure that your project is compatible with all dependencies, specifically limiting the Python version to be below 3.12 as required by `nautobot-golden-config`. This adjustment should allow you to successfully add `nautobot-golden-config` to your project. After making this change, execute `poetry update` to apply the new settings and resolve dependencies accordingly.


```
(nautobot-docker-compose-py3.10) nautobot-docker-compose$ poetry update
Updating dependencies
Resolving dependencies... (4.2s)

No dependencies to install or update

Writing lock file
(nautobot-docker-compose-py3.10) nautobot-docker-compose$ poetry add nautobot-golden-config
The following packages are already present in the pyproject.toml and will be skipped:

  - nautobot-golden-config

If you want to update it to the latest compatible version, you can use `poetry update package`.
If you prefer to upgrade it to the latest available version, you can use `poetry add package@latest`.

Nothing to add.
(nautobot-docker-compose-py3.10) nautobot-docker-compose$
```

was missing the app dependency in container

```
(nautobot-docker-compose-py3.10) nautobot-docker-compose$ poetry env info

Virtualenv
Python:         3.10.4
Implementation: CPython
Path:           /Users/jabelk/Library/Caches/pypoetry/virtualenvs/nautobot-docker-compose-gRtuJhB6-py3.10
Executable:     /Users/jabelk/Library/Caches/pypoetry/virtualenvs/nautobot-docker-compose-gRtuJhB6-py3.10/bin/python
Valid:          True

Base
Platform:   darwin
OS:         posix
Python:     3.10.4
Path:       /Users/jabelk/.pyenv/versions/3.10.4
Executable: /Users/jabelk/.pyenv/versions/3.10.4/bin/python3.10
(nautobot-docker-compose-py3.10) nautobot-docker-compose$
(nautobot-docker-compose-py3.10) nautobot-docker-compose$
(nautobot-docker-compose-py3.10) nautobot-docker-compose$ invoke cli
Running docker compose command "ps --services --filter status=running"
Running docker compose command "run --entrypoint 'bash' nautobot"
[+] Creating 2/0
 ✔ Container nautobot-docker-compose-redis-1  Cre...                                             0.0s
 ✔ Container nautobot-docker-compose-db-1     Create...                                          0.0s
[+] Running 2/2
 ✔ Container nautobot-docker-compose-redis-1  Sta...                                             0.3s
 ✔ Container nautobot-docker-compose-db-1     Starte...                                          0.3s
nautobot@5ee7bebececd:~$ python -c "import nautobot_golden_config"
Traceback (most recent call last):
  File "<string>", line 1, in <module>
ModuleNotFoundError: No module named 'nautobot_golden_config'
nautobot@5ee7bebececd:~$ exit
```


Added to dockerfile `poetry add nautobot-golden-config && \` and it worked

```
RUN cd /source && \
    poetry install --no-interaction --no-ansi && \
    poetry add nautobot-golden-config && \
    mkdir /tmp/dist && \
    poetry export --without-hashes -o /tmp/dist/requirements.txt
```