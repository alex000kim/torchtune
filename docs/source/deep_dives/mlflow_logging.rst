.. _mlflow_logging:

================
Logging to MLFlow
================

This deep-dive will guide you through how to set up logging to MLFlow in torchtune.

.. grid:: 1

    .. grid-item-card:: :octicon:`mortar-board;1em;` What this deep-dive will cover

      * How to get started with MLFlow
      * How to use the :class:`~torchtune.training.metric_logging.MLFlowLogger`
      * How to log configs, metrics, and model checkpoints to MLFlow

torchtune supports logging your training runs to `MLFlow <https://mlflow.org/>`_.
An example MLFlow workspace from a torchtune fine-tuning run can be seen in the screenshot below.

.. image:: ../_static/img/mlflow_torchtune_project.png
  :alt: torchtune workspace in MLFlow
  :width: 100%
  :align: center

.. note::

  You will need to install the :code:`mlflow` package to use this feature.
  You can install it via pip:

  .. code-block:: bash

    pip install mlflow


  You will also likely need to set up your MLFlow tracking URI and other environment variables. You can do it through the command line with:

  .. code-block:: bash

    export MLFLOW_TRACKING_URI=http://your-tracking-server:5000
    export MLFLOW_TRACKING_USERNAME=your-username
    export MLFLOW_TRACKING_PASSWORD=your-password
    export MLFLOW_EXPERIMENT_NAME=your-experiment-name
    export MLFLOW_ENABLE_SYSTEM_METRICS_LOGGING=true

Metric Logger
-------------

The only change you need to make is to add the metric logger to your config. MLFlow will log the metrics and model checkpoints for you.

.. code-block:: yaml

    # enable logging to the built-in MLFlowLogger
    metric_logger:
      _component_: torchtune.training.metric_logging.MLFlowLogger
      tracking_uri: http://your-tracking-server:5000
      experiment_name: your-experiment-name
      run_name: your-run-name

We automatically grab the config from the recipe you are running and log it to MLFlow. You can find it in the MLFlow UI under the "Params" tab.

.. note::

  Click on this sample `MLFlow project to see the logged metrics after fine-tuning <http://your-tracking-server:5000/#/experiments/1/runs/your-run-id>`_.
  The config used to train the models can be found in the "Params" tab.
