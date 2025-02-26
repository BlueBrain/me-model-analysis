> [!WARNING]
> The Blue Brain Project concluded in December 2024, so development has ceased under the BlueBrain GitHub organization.
> Future development will take place at: https://github.com/openbraininstitute/me-model-analysis

# me-model-analysis

### Repo that contains the code to run me-model-analysis using on-demand service in AWS

- It will be deployed in the docker hub image `bluebrain/me-model-analysis`
- It will be consumed by the [frontend](https://bbpgitlab.epfl.ch/project/sbo/core-web-app/-/merge_requests/1532) when we launch a validation of the single cell me-model.
- It will use the [on-demand](https://bbpgitlab.epfl.ch/cs/cloud/aws/deployment/-/merge_requests/437) service in AWS


### Build package
```bash
make docker_build
```

### Push package
You need the proper dockerhub credentials
```bash
ORIGINAL_IMG="me-model-analysis:dev"
END_IMG="bluebrain/me-model-analysis:latest"

docker tag $ORIGINAL_IMG $END_IMG
docker push $END_IMG
```

## Examples
```js
const ws = new Ws(ME_MODEL_ON_DEMAND_SVC_API_GATEWAY_URL, TOKEN);
ws.send('set_model', { model_id: MODEL_ID }); // me-model id

// You might receive "Retry later" message back until the service is up
// so you need to try again and again until you get "Processing message".

// Once the model is downloaded and ready you will get "set_model_done" message.
// after this you can just start the analysis
ws.send('run_analysis', {});

// this process will update the me-model Nexus entity.
```

## Acknowledgment
The development of this software was supported by funding to the Blue Brain Project, a research center of the École polytechnique fédérale de Lausanne (EPFL), from the Swiss government’s ETH Board of the Swiss Federal Institutes of Technology.



## Copyright
Copyright (c) 2024 Blue Brain Project/EPFL

This work is licensed under [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0.html)


