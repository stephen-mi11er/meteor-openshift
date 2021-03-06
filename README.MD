## How to use

At first, create a openshift app with nodejs-0.10 and MongoDB 3.x custom cartridge.

```bash
rhc app create openshift-appname \
  nodejs-0.10 \
  https://raw.githubusercontent.com/icflorescu/openshift-cartridge-mongodb/master/metadata/manifest.yml
```

`rhc` will automatically clones your new app.
At this point, You don't need anything of default content that is shipped by nodejs cartridge.
Remove them all.
```bash
cd openshift-appname
git rm -rf * .openshift
```

Now, We have to fetch meteor bundler from this git.

```bash
git remote add meteor-openshift -m master git@github.com:jeeeyul/meteor-openshift.git
git pull -s recursive -X theirs meteor-openshift master
```
Now, time to build your meteor app.

```bash
cd path/to/your/meteorapp
meteor build path/to/your/openshift-appname --directory --server-only
```
It will generates a `bundle` directory into your openshift app repo.


Then, push your repo and see what happens.
```bash
cd path/to/your/openshift-appname
git add --all && git commit -m "First Launch" && git push
```

That's all.


## How to update meteor app

Just replace `bundle` directory with new build, then push it.

## Enable hot deploy

If you successfully deploy your app first time, Enabling hot deploy is recommanded.

```bash
cd path/to/your/openshift-appname
touch .openshift/markers/hot_deploy
git add --all && git commit -m "First Launch" && git push
```

