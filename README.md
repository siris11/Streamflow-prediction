# Long Short-Term Memory networks for Prediction in Ungauged Basins:


1) Run the training scripts: 'train_global.sh' or 'train_pub.sh'. Options for the global script are: (i) the model type: 'lstm' or 'ealstm' (ref HESSD paper here), and (ii) the option to use catchment attributes as static input features: 'static' or 'no_static'. Options for the PUB training script are just the model type, since PUB requires catchment attributes.

These bash scripts assume that you have a certain number of GPUs available for training. If no GPUS are available for training, the 'gpu=' arguments in the runtime lines (e.g., 'python3 main.py ...') must be changed to 'gpu=-1'. The number of GPUs available on the current machine goes in line 10 (global) / 16 (PUB) and the index for the last GPU goes in line 40 (global) / 36 (PUB).

These scripts are set up to run 10 random restarts of each type of experiment. The PUB experiments use k-fold (cross-site) validation with k=12 splits. These parameters can be changed in the bash traning scripts.

Runtime progress can be monitored in the 'reports' subdirectory. Each experiment type (e.g., 'global_lstm_static') will create a separate runtime file for each restart and each k-fold split, numbered appropriately. Tail these to see real-time training progress.

2) Run the test scripts: 'run_global.py' or 'run_pub.py'. Options for these include (i) the experiment name and (ii) the GPU index that you want to run on (use -1 to indicate running on the CPU). The experiment name is the file name (less any numeric identifiers) of the training report file. Outputs from these runs are stored in CSV (human-readable) files in the './analysis/resutls/' subdirectory.

3) Run the 'extract_benchmarks.py' script to prepare the benchmark data for statistical analysis. Results will be stored in CSV (human-readable) files in the './analysis/results_data/' subdirectory.

4) In the 'analysis' subdirectory, run the 'main_performance_ensemble_only.py' or 'main_performance.py' scripts to get ensemble performance statistics or basin performance statistics, respectively. These statistics are stored in the './analysis/stats' subdirectory.

5) Run the matlab script 'main_plots.m' in the 'analysis' subdirectory to make plots like what are in the paper. Figures are stored in the './analysis/figures/' subdirectory.

