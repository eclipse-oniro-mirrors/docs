# ContinuableInfo (System API)

The **ContinuableInfo** module provides the mission continuation information to be returned when the listener for listening for the mission continuation state is registered. For details about the registration, see [on('continueStateChange')](js-apis-distributedMissionManager-sys.md#distributedmissionmanageroncontinuestatechange10).

> **NOTE**
>
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> The APIs provided by this module are system APIs.

## Attributes

**System API**: This is a system API.

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

| Name      | Type  | Readable  | Writable  | Description     |
| -------- | ------ | ---- | ---- | ------- |
| srcDeviceId | string | Yes   | Yes   | ID of the source device.|
| bundleName | string | Yes   | Yes   | Name of the bundle to which the mission belongs.|
