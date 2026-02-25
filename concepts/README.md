Modules and libraries for representation extraction and steering.
Methods modified from [RepE](https://github.com/andyzoujm/representation-engineering/tree/main)

All files, except `utils.py`, are taken from the folder `repe` of the above repo.
There are some minor modifications to `rep_reading_pipeline.py`.

```
diff -r concepts/rep_reading_pipeline.py ../representation-engineering/repe/rep_reading_pipeline.py
25,26c25,27
<             hidden_states =  hidden_states[:, rep_token, :]
<             # hidden_states_layers[layer] = hidden_states.cpu().to(dtype=torch.float32).detach().numpy()
---
>             hidden_states =  hidden_states[:, rep_token, :].detach()
>             if hidden_states.dtype == torch.bfloat16:
>                 hidden_states = hidden_states.float()
68c69
<     def _forward(self, model_inputs, rep_token, hidden_layers, rep_reader=None, component_index=0, which_hidden_states=None):
---
>     def _forward(self, model_inputs, rep_token, hidden_layers, rep_reader=None, component_index=0, which_hidden_states=None, pad_token_id=None):
```