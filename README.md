# Kubectl in Heroku

Add the kuberentes binary to Heroku

Variable ``KUBERNETES_VERSION`` or empty for latest version.
```bash
# Add
heroku buildpacks:add https://github.com/okvic77/heroku-buildpack-kubernetes

# Remove
heroku buildpacks:remove https://github.com/okvic77/heroku-buildpack-kubernetes
```

The installation is done while deploy.

For credentials, write the config file to ``KUBECONFIG`` environment variable. The credentials have to be in a YAML format, so you can encode the file in base64 and save as the variable. Then decode while your app boot and write.

## Example

```bash
heroku config:set KUBERNETES=$(cat configfile | base64)
```

```node
if (process.env.KUBERNETES) {
  var data = new Buffer(process.env.KUBERNETES, 'base64');
  fs.writeFileSync(process.env.KUBECONFIG, data.toString('utf8'), 'utf8');
}
```
