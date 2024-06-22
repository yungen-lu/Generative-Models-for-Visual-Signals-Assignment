# Generative Models for Visual Signals Assignment

# Setup

python >= 3.10

```shell
pip install -r requirements.txt
```

# How to run

1. clone the repo

2. (optional) change the example image under  `data/`

3. Run `baseline_dip.ipynb` to view the baseline result

4. Run `my_dip.ipynb` to view the experiment result

   1. choose a stage scheduler

      ```python
      # scheduler_type = "uniform"
      scheduler_type = "sharp linear increase" # <- choose one
      # scheduler_type = "log10 linspace"
      ```

   2. (optional) modify `timesteps` or `iteration` vairable to see different result

5. Run `compare_plot.ipynb` to view the comparison chart