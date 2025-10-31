# Changelog
All notable changes to this project will be documented in this file.

## 3.16.2 - 2025-10-16
### Bug fixes
* Fixed an issue where [`Geolocation`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#geolocation) data was tracked incorrectly.

## 3.16.1 - 2025-09-29
### Bug fixes
* Fixed an issue where incorrect targeting data could be selected under certain conditions.
* Changed the **Unsupported targeted condition type found** log's level to `INFO`.

## 3.16.0 - 2025-08-29
### Features
* Added an `overwrite` flag to [`CustomData`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#customdata), used as the `overwrite` parameter during tracking.
* [`CustomData`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#customdata) can now be created using a `name`, in addition to the existing method of using an `index`.
## 3.15.0 - 2025-07-23
### Features
* Added the [`evaluate_audiences`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#evaluate_audiences) method. This method iterates over all Audiences Explorer segments, evaluates each one, and tracks the segments for which the visitor is targeted using the [`TARGETINGSEGMENT`](https://developers.kameleoon.com/apis/data-api-rest/all-endpoints/post-visit-events/) event.

## 3.14.0 - 2025-06-27
### Features
* Added support for using a Custom Data value for traffic bucketing instead of the default visitor code. [Learn More](https://help.kameleoon.com/create-feature-flag/#Advanced_Flag_Settings).

## 3.13.0 - 2025-05-26
### Features
* Added support for **304 (Not Modified)** responses from the SDK config service to avoid redundant updates and reduce traffic when the configuration hasn't changed.
* Added support for a **New**/**Returning** visitor breakdown filter in reports (requires calling [`get_remote_visitor_data`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#get_remote_visitor_data)).
### Fixed
* Fixed an issue where visitor data fields - [`Browser`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#browser), [`Device`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#device), and [`OperatingSystem`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#operatingsystem) - were all retrieved from the Data API and added to the visitor, even when only a subset of them was requested.

## 3.12.1 - 2025-04-08
### Bug fixes
* Changed the order in which **conversion** and **experiment** events are sent. This may lead to more accurate **visit**-level experiment reporting.

## 3.12.0 - 2025-04-02
### Features
* Added support for new conditions:
    - Exclusive Campaign
    - Experiment
    - Personalization

## 3.11.0 - 2025-03-24
### Features
* Added new optional parameters `negative` and `metadata` to the [`track_conversion`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#track_conversion) method.
* Added new optional parameter `metadata` to the [`Conversion`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#conversion) data constructor.
* Added new configuration parameter `network_domain` to [`KameleoonClientConfig`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#create) and the [configuration](https://developers.kameleoon.com/python-sdk.html#additional-configuration) file. This parameter allows specifying a custom domain for all outgoing network requests.

## 3.10.0 - 2025-03-18
### Features
* Added support for Contextual Bandit evaluations. Calling [`get_remote_visitor_data`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#get_remote_visitor_data) with the `cbs=True` flag is required for this feature to function correctly. Platform-wide release expected in March 2025.

## 3.9.0 - 2025-02-26
### Features
* Added SDK support for **Mutually Exclusive Groups**. When feature flags are grouped into a **Mutually Exclusive Group**, only one flag in the group will be evaluated at a time. All other flags in the group will automatically return their default variation.

## 3.8.0 - 2025-02-10
### Features
* Added SDK support for **holdout experiments**. Visitors assigned to a holdout experiment are excluded from all other rollouts and experiments, and consistently receive the default variation. For visitors not in a holdout experiment, the standard evaluation process applies, allowing them to be evaluated for all feature flags as usual. Platform-wide release expected in February 2025.

## 3.7.0 - 2025-01-17
### Features
* Added support for **simulated** variations.
* Added the [`set_forced_variation()`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#set_forced_variation) method. This method allows explicitly setting a forced variation for a visitor, which will be applied during experiment evaluation.

## 3.6.1 - 2024-11-20
### Bug fixes
* Resolved an issue where the validation of [top-level domains](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#additional-configuration) for `localhost` resulted in incorrect failures. The SDK now accepts the provided domain without modification if it is deemed invalid and logs an [error](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#log-levels) to notify you of any issues with the specified domain.

## 3.6.0 - 2024-11-15
### Features
* Introduced a new `visitor_code` parameter to [`RemoteVisitorDataFilter`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#using-parameters-in-get_remote_visitor_data). This parameter determines whether to use the `visitor_code` from the most recent previous visit instead of the current `visitor_code`. When enabled, this feature allows visitor exposure to be based on the retrieved `visitor_code`, facilitating [cross-device reconciliation](https://developers.kameleoon.com/core-concepts/cross-device-experimentation/). Default value of the parameter is `True`.
### Bug fixes
* Fixed an issue with the [`Page URL`](https://developers.kameleoon.com/feature-management-and-experimentation/using-visit-history-in-feature-flags-and-experiments/#benefits-of-calling-getremotevisitordata) and [`Page Title`](https://developers.kameleoon.com/feature-management-and-experimentation/using-visit-history-in-feature-flags-and-experiments/#benefits-of-calling-getremotevisitordata) targeting conditions, where the condition evaluated all previously visited URLs in the session instead of only the current URL, corresponding to the latest added [`PageView`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#pageview).<br/>
**NOTE**: This change may impact your existing targeting. Please review your targeting conditions to ensure accuracy.

## 3.5.0 - 2024-10-04
### Features
* Introduced new evaluation methods for clarity and improved efficiency when working with the SDK:
  - [`get_variation`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#get_variation)
  - [`get_variations`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#get_variations)
* These methods replace the deprecated ones:
  - [`get_feature_variation_key`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#get_feature_variation_key)
  - [`get_feature_variable`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#get_feature_variable)
  - [`get_active_features`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#get_active_features)
  - [`get_feature_variation_variables`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#get_feature_variation_variables)
* A new version of the [`is_feature_active`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#is_feature_active) method now includes an optional `track` parameter, which controls whether the assigned variation is tracked (default: `True`).
* Enhanced the [`get_engine_tracking_code`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#getenginetrackingcode) method to properly handle `JS` and `CSS` variables.

## 3.4.0 - 2024-09-05
### Features
* Improved the tracking mechanism to consolidate multiple visitors into a single request, combining information on all affected visitors into one request, sent once per interval.
* Added a new parameter `instant` of the [`flush`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#flush) method. If the parameter's value is `True` the visitor's data is tracked instantly. Otherwise, the visitor's data will be tracked with next tracking interval. Default value of the parameter is `False`.
* Added new configuration parameter `tracking_interval_millisecond` to [`KameleoonClientConfig`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#initializing-the-kameleoon-client) and the [configuration](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#additional-configuration) file, which is used to set interval for tracking requests. Default value is `1000` milliseconds.
* New Kameleoon Data type [`UniqueIdentifier`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#uniqueidentifier) is introduced. It will be used in all methods instead of `is_unique_identifier` parameter. All usages of the `is_unique_identifier` parameter in the methods are marked as deprecated:
    - [`flush`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#flush)
    - [`track_conversion`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#track_conversion)
    - [`track_conversion`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#track_conversion)
    - [`get_feature_variation_key`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#get_feature_variation_key)
    - [`get_feature_variable`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#get_feature_variable)
    - [`is_feature_active`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#is_feature_active)
    - [`get_remote_visitor_data`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#get_remote_visitor_data)
* Enhanced [logging](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#logging):
  - Introduced [log levels](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#log-levels):
    - `NONE`
    - `ERROR`
    - `WARNING`
    - `INFO`
    - `DEBUG`
  - Added support for [custom logger](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#custom-handling-of-logs) implementations.
* Changed the parameters `logger` and `multi_threading` in object [`KameleoonClientConfig`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#initializing-the-kameleoon-client) the deprecated.
* Enhanced top-level domain validation within the SDK. The implementation now includes automatic trimming of extraneous symbols and provides a [warning](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#log-levels) when an invalid domain is detected.
### Bug fixes
* Resolved an issue where the [`flush(None, is_unique_identifier)`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#flush) method was incorrectly sending requests with `is_unique_identifier` applied to each visitor. Now, `is_unique_identifier` is only considered if `visitor_code` is provided and not None.
* Fixed an issue that caused duplicate entries in feature flag results for both anonymous and authorized/identified visitors during data reconciliation. This problem occurred when custom data of type mapping ID was not consistently sent for all sessions.

## 3.3.3 - 2024-07-03
### Bug fixes
* Resolved issues with malformed library package assembly.

## 3.3.2 - 2024-07-02
### Features
* This version broadens the range of acceptable `pyyaml` and `sseclient-py` versions, enhancing flexibility and compatibility with more recent releases of the library:
- Expanded the compatible versions of the `pyyaml` library to include `6.0.*`, in addition to the previously supported `5.4.*`.
- Expanded the compatible versions of the `sseclient-py` library to include `1.8.*`, in addition to the previously supported `1.7.*`.

## 3.3.1 - 2024-07-01
### Features
* Expanded the compatible versions of the `aiohttp` library to include `3.9.*`, in addition to the previously supported `3.8.*`. This version broadens the range of acceptable `aiohttp` versions, enhancing flexibility and compatibility with more recent releases of the library.

## 3.3.0 - 2024-06-21
### Features
* The [Likelihood to convert](https://developers.kameleoon.com/feature-management-and-experimentation/using-visit-history-in-feature-flags-and-experiments) targeting condition is now available. Pre-loading the data is required using [`get_remote_visitor_data`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#get_remote_visitor_data) with the `kcs` parameter set to `True`.
### Bug fixes
* The SDK no longer logs failed tracking requests to the [Data API](https://developers.kameleoon.com/apis/data-api-rest/all-endpoints/post-visit-events/) when the user agent is identified as a bot (i.e., when the status code is 403).

## 3.2.0 - 2024-06-10
### Features
* New targeting conditions are now available (some of them may require [`get_remote_visitor_data`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk#getremotevisitordata) pre-loaded data)
  - Browser Cookie
  - Operating System
  - IP Geolocation
  - Kameleoon Segment
  - Target Feature Flag
  - Previous Page
  - Number of Page Views
  - Time since First Visit
  - Time since Last Visit
  - Number of Visits Today
  - Total Number of Visits
  - New or Returning Visitor
* New Kameleoon Data types were introduced:
  - [`Cookie`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#cookie)
  - [`OperatingSystem`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#operatingsystem)
  - [`Geolocation`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#geolocation)
* Added [`get_active_features`](https://developers.kameleoon.com/python-sdk.html#get_active_features) method uses for obtaining a information about the active feature flags that are available for the visitor.
* Method [`get_active_feature_list_for_visitor`](https://developers.kameleoon.com/python-sdk.html#get_active_feature_list_for_visitor) is deprecated
### Bug fixes
* Stability and performance improvements.
* Changed the parameter `title` in object [`PageView`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#pageview) to optional.

## 3.1.0 - 2024-02-29
### Features
* Added support for additional Data API servers across the world for even faster network requests.
* Increased limit for requests to Data API: [rate limits](https://developers.kameleoon.com/apis/data-api-rest/overview/#rate-limits)
* Added [`get_visitor_warehouse_audience`](https://developers.kameleoon.com/python-sdk.html#get_visitor_warehouse_audience) method to retrieve all data associated with a visitor's warehouse audiences and adds it to the visitor.

## 3.0.0 - 2024-01-25
### Breaking changes
* You should no longer create a new `KameleoonClient` instance explicitly. To get an instance of `KameleoonClient`, call [`KameleoonClientFactory.create`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#create) instead.
* A new `KameleoonClient` instance does not await full initialization anymore. Instead, new `wait_init` and `wait_init_async` methods allow you to check whether the client has been successfully initialized before executing other operations.
* Renamed `get_feature_all_variables` method to [`get_feature_variation_variables`](https://developers.kameleoon.com/python-sdk.html#get_feature_variation_variables)
* Removed all deprecated methods and errors related to **experiments**:
  * Methods:
    - `trigger_experiment`
    - `get_variation_associated_data`
    - `get_experiment_list`
    - `get_experiment_list_for_visitor`
  * Error types:
    - `ExperimentConfigurationNotFound`
    - `NotTargeted`
    - `NotAllocated`
    - `SiteCodeDisabled`
* Removed additional deprecated methods:
    - `obtain_visitor_code`
    - `obtain_variation_associated_data`
    - `obtain_experiment_list`
    - `obtain_feature_variable`
    - `obtain_feature_list`
    - `obtain_feature_all_variables`
    - `retrieve_data_from_remote_source`
* Changed `KameleoonClientConfig` (previously named `KameleoonClientConfiguration`):
    - Renamed `KameleoonClientConfiguration` to `KameleoonClientConfig`
    - Added required parameters `client_id` and `client_secret` (`ConfigCredentialsInvalid` is raised unless `client_id` and `client_secret` are specified and non-empty)
    - Removed `visitor_data_maximum_size` parameter
    - Added `session_duration_minute` parameter
    - Added `top_level_domain` parameter
    - Renamed `actions_configuration_refresh_interval` parameter to `refresh_interval_minute`
    - Renamed `default_timeout` parameter to `default_timeout_millisecond`
* Changed data:
  * `Browser`:
    - Changed `browser_type`, `version` fields to read-only
  * `Conversion`:
    - Changed `goal_id`, `revenue`, `negative` fields to read-only
  * `CustomData`:
    - Changed `id` field to read-only
    - Changed the data type of the `id` field to `int`
    - Removed the deprecated `value` constructor parameter
  * `Device`:
    - Changed `device_type` field to read-only
  * `PageView`:
    - Changed `url`, `title`, `referrers` fields to read-only
  * `UserAgent`:
    - Changed `value` field to read-only
    - Removed `get_value` method
* Changed the `cookies` parameter type in [`get_visitor_code`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#get_visitor_code) to `Dict[str, Morsel[str]]`.
* Changed errors:
  * Added new exception `FeatureEnvironmentDisabled` indicating that the feature flag is disabled for certain environments. The following methods can throw the new exception:
    - [`get_feature_variation_key`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#get_feature_variation_key)
    - [`get_feature_variable`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#get_feature_variable)
    - [`get_feature_variation_variables`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#get_feature_variation_variables)
  * Added `SiteCodeIsEmpty` exception, which the [`KameleoonClientFactory.create`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#create) method raises if the specified site code parameter is empty.
  * Renamed error types:
    - `ConfigurationNotFoundException` to `ConfigFileNotFound`
    - `CredentialsNotFoundException` to `ConfigCredentialsInvalid`
    - `VisitorCodeNotValid` to `VisitorCodeInvalid`
    - `FeatureConfigurationNotFound` to `FeatureNotFound`
    - `VariationConfigurationNotFound` to `FeatureVariationNotFound`
    - `KameleoonException` to `KameleoonError`
### Features
* Implemented [`KameleoonClientFactory`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#kameleoonclientfactory) to manage `KameleoonClient` instances:
    - [`create`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/create)
    - [`forget`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#forget)
* Added [`set_legal_consent`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/python-sdk/#set_legal_consent) method to determine the types of data Kameleoon includes in tracking requests. This helps you adhere to legal and regulatory requirements while responsibly managing visitor data. You can find more information in the [Consent management policy](https://help.kameleoon.com/consent-management-policy/).

## 2.4.0 - 2023-09-14
### Features
* Added [`get_remote_visitor_data`](https://developers.kameleoon.com/python-sdk.html#get_remote_visitor_data) method to fetch a visitor's remote data (with an optional capability to add the fetched data to the visitor)
* Added [`get_remote_visitor_data_async`](https://developers.kameleoon.com/python-sdk.html#get_remote_data_async) method as an asynchronous variant of [`get_remote_visitor_data`](https://developers.kameleoon.com/python-sdk.html#get_remote_visitor_data) method
### Bug fixes
* Fixed an issue where the SDK wouldn't send tracking data if multi-threading was enabled.


## 2.3.0 - 2023-08-14
### Features
* Added [`get_remote_data_async`](https://developers.kameleoon.com/python-sdk.html#get_remote_data_async) method as an asynchronous variant of [`get_remote_data`](https://developers.kameleoon.com/python-sdk.html#get_remote_data) method
* Added new conditions for targeting:
    - `Visitor Code`
    - `SDK Language`
    - `Explicit Trigger`
    - [`Page Title & Page Url`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#pageview)
    - [`Browser`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#browser)
    - [`Device`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#device)
    - [`Conversion`](https://developers.kameleoon.com/feature-management-and-experimentation/web-sdks/java-sdk/#trackconversion)

## 2.2.0 - 2023-04-25

### Features

* Added a new method:
    - [`get_engine_tracking_code`](https://developers.kameleoon.com/python-sdk.html#get_engine_tracking_code) which can be used to simplify utilization of hybrid mode
* Renaming of methods:
    - `obtain_feature_variable` -> [`get_feature_variable`](https://developers.kameleoon.com/python-sdk.html#get_feature_variable)
    - `retrieve_data_from_remote_source` -> [`get_remote_date`](https://developers.kameleoon.com/python-sdk.html#get_feature_variable)
* The method `obtain_feature_variable` has been updated to only accept a `str` type for the `feature_key` argument. Previously, it accepted both `str` and `int` types as a `Union[str, int]` argument, but this functionality is now deprecated.
* Added possibility for [`CustomData`](https://developers.kameleoon.com/python-sdk.html#customdata) to use variable argument list of values

## 2.1.0 - 2023-02-02
* Added support of new feature flag rules:
    - [`get_feature_variation_key`](https://developers.kameleoon.com/python-sdk.html#get_feature_variation_key)
    - [`get_feature_variable`](https://developers.kameleoon.com/python-sdk.html#get_feature_variable)
    - [`get_feature_all_variables`](https://developers.kameleoon.com/python-sdk.html#get_feature_all_variables)
    - `activate_feature` -> [`is_feature_active`](https://developers.kameleoon.com/python-sdk.html#is_feature_active)
* Renaming of methods (old methods warn you on using and will be removed later)
    - `obtain_visitor_code` -> [`get_visitor_code`](https://developers.kameleoon.com/python-sdk.html#get_visitor_code)
    - `obtain_variation_associated_data` -> [`get_variation_associated_data`](https://developers.kameleoon.com/python-sdk.html#get_variation_associated_data),
    - `obtain_feature_all_variables` -> [`get_feature_all_variables`](https://developers.kameleoon.com/python-sdk.html#get_feature_all_variables),
    - `obtain_experiment_list` -> [`get_experiment_list`](https://developers.kameleoon.com/python-sdk.html#get_experiment_list) & [`get_experiment_list_for_visitor`](https://developers.kameleoon.com/python-sdk.html#get_experiment_list_for_visitor),
    - `obtain_feature_list` -> [`get_feature_list`](https://developers.kameleoon.com/python-sdk.html#get_feature_list) & [`get_active_feature_list_for_visitor`](https://developers.kameleoon.com/python-sdk.html#get_active_feature_list_for_visitor),
* Renaming of exceptions:
    - `NotActivated` -> `NotAllocated`
* Added possibility to set [`UserAgent`](https://developers.kameleoon.com/python-sdk.html#useragent).
* Removed `blocking` parameter (blocking mode) [`KameleoonClient`](https://developers.kameleoon.com/python-sdk.html#initializing-the-kameleoon-client) init method

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
