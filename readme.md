# next-aws-lambda-webpack-plugin

[![npm puppeteer package](https://img.shields.io/npm/v/next-aws-lambda-webpack-plugin.svg)](https://www.npmjs.com/package/next-aws-lambda-webpack-plugin)
[![integration test next@latest](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/workflows/integration%20test%20next@latest/badge.svg?branch=master)](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/actions)

This plugin will generate aws-lambda compatible function for each [Next.JS pages](https://nextjs.org/docs/basic-features/pages).
After that, you can to use theses functions with the [AWS cloudformation template](https://aws.amazon.com/cloudformation/resources/templates/) or/and [AWS serverless template](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html).

This plugin use [next-aws-lambda](https://www.npmjs.com/package/next-aws-lambda) package,
create by and for the [serverless](https://serverless.com/) community :heart:.

:point_right: **[Here a full implementation example (step by step)](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/blob/master/example/readme.md)**

![next-aws-lambda-webpack-plugin](./assets/next-aws-lambda-webpack-plugin.png)

### Requirement

1. Use [Next.JS](https://nextjs.org/docs/getting-started) CLI for build your project (`next build`)
   - The configuration file [next.config.js](https://nextjs.org/docs/api-reference/next.config.js/build-target) must use `target: 'serverless'`.
2. Use [SAM](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html) or [AWS CLI cloudformation](https://docs.aws.amazon.com/cli/latest/reference/cloudformation/index.html) for your deployment.

### Next.JS compatibility

| Next.JS Version | Tests                                                                                                                                                                                                                                                  |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| canary          | [![integration test next@canary](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/workflows/integration%20test%20next@canary/badge.svg)](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/actions)               |
| latest          | [![integration test next@latest](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/workflows/integration%20test%20next@latest/badge.svg?branch=master)](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/actions) |
| 10.0.0          | [![integration test next@latest](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/workflows/integration%20test%20next@10.0.0/badge.svg?branch=master)](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/actions) |
| 9.5.0           | [![integration test next@latest](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/workflows/integration%20test%20next@9.5.0/badge.svg?branch=master)](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/actions)  |
| 9.4.0           | [![integration test next@latest](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/workflows/integration%20test%20next@9.4.0/badge.svg?branch=master)](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/actions)  |

# Install

Use npm :

```
npm install --save-dev next-aws-lambda-webpack-plugin
```

Add the plugin to the Next.JS ([next.config.js](https://nextjs.org/docs/api-reference/next.config.js/custom-webpack-config)) configuration file.

| Plugin Arguments | Required | Description                                                                                                                                   |
| ---------------- | :------: | --------------------------------------------------------------------------------------------------------------------------------------------- |
| nextJsConfig     |   YES    | Next.JS config retrieve from#[next.config.js](https://nextjs.org/docs/api-reference/next.config.js/custom-webpack-config), see example below. |
| options          |    NO    | [see options](#options)                                                                                                                       |

Example:

```Javascript
const GenerateAwsLambda = require('next-aws-lambda-webpack-plugin');

module.exports = {
    target: 'serverless',
    webpack: (config, nextConfig) => {
        config.plugins.push(new GenerateAwsLambda(nextConfig));
        return config
    },
};
```

#### Options

| Plugin Options | Required | Default      | Description                                                                               |
| -------------- | -------- | ------------ | ----------------------------------------------------------------------------------------- |
| distDir        | No       | "out_lambda" | Custom lambda build directory.                                                            |
| prefix         | No       | "l"          | Prefix apply to each lambda directory.                                                    |
| pages          | No       | []           | A whitelist who specified SSR pages. If empty array is specified all pages are generated. |

Example:

```Javascript
//...snip...
new AwsLambdaGenerator(nextConfig,{
    distDir: 'lambda_build'
})
//...snip...
```

# Architecture Example

:point_right: **[Go to example](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/blob/master/example/readme.md)**

[![cloud-front-distribution-example](./assets/cloud-front-distribution-example.png)](https://github.com/vincent-herlemont/next-aws-lambda-webpack-plugin/blob/master/example/readme.md)
