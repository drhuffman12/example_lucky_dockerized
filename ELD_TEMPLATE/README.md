# Example Lucky Dockerized

## In your Host OS shell

### Copy this repo
`git clone git@github.com:drhuffman12/example_lucky_dockerized.git`

<!-- ### Rename the folder (as desired)

```
mv example_lucky_dockerized/ $YOUR_APP_NAME
cd $YOUR_APP_NAME
``` -->

### Copy template files

`cp -R ./ELD_TEMPLATE/01/** .`

### Start the container

```
host_os/dc_clean
host_os/dc_build
host_os/dc_sh
```

## In your Container shell

### Init your app or API

(See also: https://luckyframework.org/guides/getting-started/starting-project)

```
lucky init
```

... Then, follow along; e.g.:

```
$ lucky init
Welcome to Lucky v0.25.0 🎉

Project name?: my_app
...
API only or full support for HTML and Webpack? (api/full): full
...
Generate authentication? (y/n): y
...
Done generating your Lucky project

  ▸ cd into my_app
  ▸ check database settings in config/database.cr
  ▸ run script/setup
  ▸ run lucky dev to start the server
```

NOTE: If you entered anything OTHER THAN `my_app`, then you'll need to replace `my_app` in various places in the docker files and your app's code!

### Config/build/launch as applicable

▸ `cd my_app`
▸ (OPTIONALLY) check database settings in config/database.cr
* # `shards install`
* # `shards update`
* # `shards build`

* Edit the `shards.yml` file to look like:
  ```
  ...
  targets:
  my_app:
    main: src/my_app.cr

  start_server:
    main: src/start_server.cr

  lucky.exec:
    main: lib/lucky/src/precompiled_tasks/exec.cr
  lucky.watch:
    main: lib/lucky/src/precompiled_tasks/watch.cr
  lucky.gen.model:
    main: lib/lucky/src/precompiled_tasks/gen/model.cr
  lucky.gen.action:
    main: lib/lucky/src/precompiled_tasks/gen/action/helpful_error.cr
  lucky.gen.action.browser:
    main: lib/lucky/src/precompiled_tasks/gen/action/browser.cr
  lucky.gen.action.api:
    main: lib/lucky/src/precompiled_tasks/gen/action/api.cr
  lucky.gen.resource.browser:
    main: lib/lucky/src/precompiled_tasks/gen/resource/browser.cr
  lucky.gen.page:
    main: lib/lucky/src/precompiled_tasks/gen/page.cr
  lucky.gen.component:
    main: lib/lucky/src/precompiled_tasks/gen/component.cr
  # lucky.gen.task:
  #   main: lib/lucky/src/precompiled_tasks/gen/task.cr
  lucky.secret_key:
    main: lib/lucky/src/precompiled_tasks/gen/secret_key.cr

  # crystal: 0.35.1
  ...
  ```
  ... Or, possibly just run `cp container_os/shard.yml ./` (but compare first in case you customized anything).

▸ `script/setup`
▸ run `lucky dev` to start the server

### Testing

TODO: See: https://luckyframework.org/guides/testing/introduction

TODO: Adjust the scripts to allow connecting to an existing/running container. Meanwhile...

If you're running `lucky dev`, exit out via `CTRL-C`.

Then, type `crystal spec`.

## In your browser

When you succesfully run `lucky dev`, it will tell you something like: `🎉 App running at http://127.0.0.1:3001`.

However, when running in the Docker container, and browsing the app from your Host OS, you'll actually need to browse to: `http://172.30.0.4:3001`
