# Changelog
All notable changes to this project will be documented in this file.

## 2.0.0 - 2022-10-21
* Added update campaigns and feature flag configurations instantaneously with Real-Time Streaming Architecture: [`Documentation`](https://developers.kameleoon.com/python-sdk.html#streaming) or [`Product Updates`](https://www.kameleoon.com/en/blog/real-time-streaming)
* Added a new method [`on_update_configuration`](https://developers.kameleoon.com/python-sdk.html#on_update_configuration) to handle events when configuration data is updated in real time.
* Significantly improved configuration load time
* Fixed an issue which can be a reason if crash during initialization.
* Added support for **Experiment** & **Exclusive Campaign** conditions. Related to [`trigger_experiment`](https://developers.kameleoon.com/python-sdk.html#trigger_experiment)
* Added method to obtain a list of feature flags: [`obtain_feature_list`](https://developers.kameleoon.com/python-sdk.html#obtain_feature_list)
* Added method to obtain a list of experiments: [`obtain_experiment_list`](https://developers.kameleoon.com/python-sdk.html#obtain_experiment_list)
* [`client_id and client_secret`](https://developers.kameleoon.com/python-sdk.html#additional-configuration) is deprecated and not required anymore.
* Added method to obtain all variables for feature flag: [`obtain_feature_all_variables`](https://developers.kameleoon.com/python-sdk.html#obtain_feature_all_variables)
* Added KameleoonData [`Device`](https://developers.kameleoon.com/python-sdk.html#device) data. Possible values are: **PHONE**, **TABLET**, **DESKTOP**.
* Removed KameleoonData `Interest`
* Added support of `is among the values` operator for Custom Data

## 1.0.9 - 2022-08-16
* Fixed crash when passing invalid credentials [`client_id and client_secret`](https://developers.kameleoon.com/python-sdk.html#additional-configuration)
* Added timeout for all network requests 

## 1.0.8 - 2022-08-08
* Added [`multi_threading`](https://developers.kameleoon.com/python-sdk.html#additional-configuration) parameter to work in multi-threading environment. By default SDK works in a single thread to avoid GIL's performance issues.

## 1.0.7 - 2022-07-26
* Removed extra logging

## 1.0.6 - 2022-07-05
* Updated package's dependencies

## 1.0.5 - 2022-06-23
* Added [`configuration_object`](https://developers.kameleoon.com/python-sdk.html#additional-configuration) parameter as a way to setup KameleoonClient

## 1.0.4 - 2022-06-14
* Fixed issue when [`add_data`](https://developers.kameleoon.com/python-sdk.html#add_data) accepts only first one parameter and ignores others

## 1.0.3 - 2022-04-12
* Added method for retrieving data from remote source: [`retrieve_data_from_remote_source`](https://developers.kameleoon.com/python-sdk.html#retrieve_data_from_remote_source)

## 1.0.2 - 2022-02-15
* Added support of multi-environment for feature flags, Related to [`activate_feature`](https://developers.kameleoon.com/python-sdk.html#activate_feature), [`obtain_feature_variable`](https://developers.kameleoon.com/python-sdk.html#obtain_feature_variable)
* Added checking for status of site_code (Enable / Disable). Related to [`activate_feature`](https://developers.kameleoon.com/python-sdk.html#activate_feature), [`trigger_experiment`]( https://developers.kameleoon.com/python-sdk.html#trigger_experiment)

## 1.0.1 - 2022-01-13
* Added scheduling functionality for [`activate_feature`](https://developers.kameleoon.com/python-sdk.html#activate_feature)
* Fixed issues in [`activate_feature`]( https://developers.kameleoon.com/python-sdk.html#activate_feature ), [`trigger_experiment`]( https://developers.kameleoon.com/python-sdk.html#trigger_experiment ),  [`obtain_feature_variable`]( https://developers.kameleoon.com/python-sdk.html#obtain_feature_variable )

## 1.0.0 - 2021-10-19
* Added WSGI middleware
