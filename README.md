A simple example of exporting a [transformer](https://huggingface.co/docs/transformers/index) model with Python, then loading it into tract to make predictions.

# To Use

First export the pre-trained transformer model using Python and PyTorch

``` shell
python export.py
```

the exported model and tokenizer are saved in `./albert`. Then build the wasm module for deployment in Redpanda

``` rust
cargo build --release --target=wasm32-wasi
```

Deploy the model into Redpanda!

``` text
rpk wasm deploy --file ./target/wasm32-wasi/release/albert-qa-wasi.wasm \
  --input-topic <> \
  --output-topic <> \
  --var CONTENT='My name is Albert and I live in the broker.'
```
