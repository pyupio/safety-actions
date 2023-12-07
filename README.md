# Safety CLI 3 GitHub Action

A [GitHub Action](https://github.com/features/actions) for using [Safety](https://safetycli.com) to check for
vulnerabilities in your projects. This Action is based on Safety CLI 3.

You can use the Action as follows:

```yaml
name: Example workflow for Python using Safety Action
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - name: Run Safety CLI to check for vulnerabilities
        uses: pyupio/safety-3-beta/safety-3@main
        with:
          api-key: ${{ secrets.SAFETY_API_KEY }}

```

### Getting a Safety API key

To get a Safety API key, [create a Safety account](https://manage.safetycli.com/create-account/) (includes a free trial). 

Once you have a Safety API key, [set it as a GitHub secret](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions) and reference it in your Action using `${{ secrets.SAFETY_API_KEY }}`, replacing `SAFETY_API_KEY` with the name you used for the GitHub secret.

### Properties

The Safety Action has the following properties. Safety's CLI's default settings can be overridden using the `args` property. To learn more see [Safety 3 documentation](https://docs.safetycli.com/safety-docs/)

| Property          | Default | Description                                                                                             |
| --------          | ------- | ---------------------------------------------------------------------------------------------------     |
| api-key           |         | Your Safety API Key                                                                                     |
| continue-on-error | false   | Set to yes/true to always return a zero (success/pass) exit code                                        |
| output-format     | screen  | Options are: screen, json, html, spdx, none                                                             |
| args              |         | Override the default arguments to Safety CLI 3.                                                         |

Here is another example of the Action showing `continue-on-error` and `args` properties:

```yaml
name: Example workflow customizing the Safety Action
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - name: Run Safety CLI to check for vulnerabilities
        uses: pyupio/safety-3-beta/safety-3@main
        with:
          api-key: ${{ secrets.SAFETY_API_KEY }}
          continue-on-error: true # Do not fail this action if vulnerabilities are found
          args: --detailed-output # To always see detailed output from this action

```

### Documentation and support

For detailed documentation on Safety, head over to our [documentation portal](https://docs.safetycli.com/safety-docs/). If you need help or have questions, reach out at support@safetycli.com

Made with 💜 by Safety Cybersecurity