# BAREC_Arabic_Readability_Assessment
We treat readability level prediction for a sentence as a regression
problem. We use a two-phase training schedule
with distinct losses.
In Phase 1, We fine-tune the
AraBERT-v2 pretrained model in mixed-precision
mode for 6 epochs with a batch size of 64. An
AdamW optimizer minimizes the Mean Squared Error (MSE) between the scalar prediction ˆy and the
gold label y using a learning rate of 2 × 10−5 with
linear warm-up over 10% of the total updates. We
consider the best checkpint on validation set, which
is the third epoch, then, in Phase 2, we switch to
the differentiable QWK objective (SoftQWKLoss):
each ˆy is converted to a Gaussian-smoothed distribution over the 19 levels, a soft confusion matrix
is accumulated, and we minimize 1 − κ so that optimization is aligned with the leaderboard metric.
For evaluation, from the raw scalar ˆy we report MSE, MAE, and R2. For ordinal metrics, we
round and clip ˆy to the range [1, 19] and compute
QWK, tolerance-1 accuracy (AdjAcc19), exact 19way accuracy (Acc19), and coarse-bin accuracies
(Acc7/Acc5/Acc3) obtained by collapsing the 19
levels into 7/5/3 groups.