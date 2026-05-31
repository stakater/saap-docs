# Develop

This section covers the inner development loop on {{ product_name }} — writing code locally, iterating against a real cluster, debugging, and following production-ready practices.

## How it works

You run your application locally with [Tilt](../managed-addons/tilt/index.md), which builds and redeploys your container on every code change directly into your sandbox namespace on the cluster. You debug against live cluster traffic with [mirrord](../managed-addons/mirrord/index.md) instead of recreating production conditions on your laptop. The full local-to-cluster loop is set up once and then stays out of your way.

## What you do

Start with the [Inner Loop](./tutorials/inner-loop/prepare-environment/prepare-env.md) tutorial series — twenty-plus steps that walk through preparing your environment, containerising your app, deploying to your sandbox, exposing it, monitoring it, and scaling it. The [Tilt zero-to-hero guide](./tutorials/inner-loop/tilt-zero-to-hero/step-by-step-guide.md) is the condensed end-to-end version.

For deeper context before you start, read [Inner vs outer loop](./explanation/inner-outer-loop.md) and [Local development workflow](./explanation/local-development-workflow.md). When you are ready to ship outside the inner loop, continue to [Deploy](../deploy/index.md) for the outer-loop / GitOps delivery path.

## Next step

Continue to [Prepare the local environment](./tutorials/inner-loop/prepare-environment/prepare-env.md) to set up Tilt and your sandbox.
