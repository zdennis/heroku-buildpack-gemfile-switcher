This buildpack enables you to set the Gemfile when deploying on Heroku by setting a GEMFILE env var.

It needs to be inserted before the heroku-buildpack-ruby buildpack.

## How does it work?

Set the GEMFILE env var for your Heroku app to the relative path of the gemfile you want to use, e.g.:

```bash
heroku config:set GEMFILE=gemfiles/rails_3.gemfile
```

Upon deploy this will run the following commands:

```bash
ln -sf gemfiles/rails_3.gemfile Gemfile
ln -sf gemfiles/rails_3.gemfile.lock Gemfile.lock
```

Both the target gemfile and lock file must exist otherwise this will fail and neither will be symlinked.

## Why does this have to be inserted before heroku-buildpack-ruby?

Because the gemfile switching needs take place before the ruby buildpack tries to bundle or run any commands that would depend on bundler running such as asset precompilation.
