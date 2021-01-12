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

(See: https://luckyframework.org/guides/getting-started/starting-project)

`lucky init` and follow along; e.g.:

```
$ lucky init
Welcome to Lucky v0.25.0 🎉

Project name?: example_lucky_dockerized
...
API only or full support for HTML and Webpack? (api/full): full
...
Generate authentication? (y/n): y
...
Done generating your Lucky project

  ▸ cd into example_lucky_dockerized
  ▸ check database settings in config/database.cr
  ▸ run script/setup
  ▸ run lucky dev to start the server
```
