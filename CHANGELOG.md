# Changelog
All notable changes to this project will be documented in this file.

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
