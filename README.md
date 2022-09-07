# TeX Live buildpack for Scalingo

This is a [buildpack][buildpacks] to run [TeX Live][tl] inside a dyno.

### How does it work?

- In this form, it uses [install-tl][install-tl] it installs a working TeX Live
  into your application into your Heroku app.
- It installs `scheme-small` to have a working minimal setup.
- It uses [tlmgr][tlmgr] to install custom packages.
- On subsequent pushes it uses [tlmgr][tlmgr] to update all installed packages.

Since we are not using a prepackaged version of TeX Live, the initial install
can take some time. But in doing so you also gain more freedom with the
selection of your packages.

### Custom packages

You can add a file called `texlive.packages` in your repo:

```text
collection-bibtexextra
collection-fontsextra
collection-langgerman
collection-xetex
```

It looks similar to the default `texlive.profile`, but without the `1` or `0`
at the end. The buildpack runs `tlmgr install` on every line in this file. So
you can use single packages or these collections.

### Custom TeX Live version

By default the latest TeX Live version will be installed. You can customize the
path to the repository to be used by adding a file called `texlive.repository`
to your project. It should contain only the path to the location of the TeX Live
repository that you want to use without trailing `/`. For example:

```text
ftp://tug.org/historic/systems/texlive/2016/tlnet-final
```

This will install the latest TeX Live 2016 release.


[tl]: https://www.tug.org/texlive/
[buildpacks]: https://doc.scalingo.com/platform/deployment/buildpacks/intro
[install-tl]: http://www.tug.org/texlive/doc/install-tl.html
[tlmgr]: http://www.tug.org/texlive/tlmgr.html
