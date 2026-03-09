# Agent guidelines

## Testing

When updating tests for new spaCy or model versions (e.g. 3.7/3.8):

1. **Prefer conditional assertions over exclusions.** Do not add or keep model exclusions (`excluded_nlps`, `excluded_nlps_3_7_plus`, etc.) when the same case can be covered by a conditional or alternative expected value (e.g. `expected_*_3_7_plus`, `alternative_expected_*`). Use version-gated or model-specific expected values so that every supported model is still asserted for that scenario where feasible.

2. **Do not encode regressions.** Do not add or change expected values so that tests pass by asserting on worse or incorrect model behavior. If a new model output is linguistically wrong (e.g. wrong referent, wrong morphology, or a parse error), do not adopt that output as the new expected value and exclude models that still behave correctly. Prefer keeping the correct expectation and either fixing the model/pipeline or documenting the regression; use alternative expected values only when multiple outputs are linguistically valid (e.g. parse variation), not when one is a clear regression.

3. **Fix the cause, don’t disable the test.** If a model returns the wrong value, investigate and fix the root cause (e.g. language rules, training data, or pipeline behavior) so the model passes the correct expectation. Do not add or keep exclusions solely to make the test pass; use exclusions only as a temporary measure while a fix is in progress, or when the failure is outside our control (e.g. upstream spaCy model bug with no workaround).