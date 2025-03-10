#Attention_Pooling #Transformer

# Multi Head Attention Pooling


### Saving memory by removing [class] token

we evaluate global average pooling (GAP) and multihead attention pooling (MAP) [25] to aggregate representation from all patch tokens.

We set the number of heads in MAP to be equal to the number of attention heads in the rest of the model. To further simplify the head design we remove final non-linear projection before the final prediction layer, which was present in the original ViT paper.

Reference:
X. Zhai, A. Kolesnikov, N. Houlsby, and L. Beyer, “Scaling Vision Transformers,” Jun. 20, 2022, _arXiv_: arXiv:2106.04560. doi: [10.48550/arXiv.2106.04560](https://doi.org/10.48550/arXiv.2106.04560).