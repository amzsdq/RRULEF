# Boundary stress under the current observed idle

The earlier boundary-frequency model used a retained post-anchor mean idle of 178.15 sec as a descriptive exposure estimate. The newly closed boundary is 624 sec, about 3.50x that retained mean.

This does not make scheduler jitter a treatment variable. It strengthens the amortization requirement: when a boundary happens to be expensive, prematurely creating another boundary after ~60 sec of useful work is even more costly.

Holding 624 sec only as a sensitivity condition, 600 sec of total useful work split into ten 60-sec windows would expose the workload to roughly 6240 sec of idle; one 600-sec window would expose it once. Actual future idle is stochastic, so these are not forecasts. They isolate boundary-count leverage.

Conclusion for the current experiment: continue chaining bounded useful tasks; do not manufacture handoffs for measurement density.