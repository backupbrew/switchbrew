# acc:su

This is
"nn::account::IAccountServiceForAdministrator".

| Cmd | Name                                                     |                                                                                          |
| --- | -------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| 0   | GetUserCount                                             |                                                                                          |
| 1   | GetUserExistence                                         |                                                                                          |
| 2   | ListAllUsers                                             |                                                                                          |
| 3   | ListOpenUsers                                            |                                                                                          |
| 4   | GetLastOpenedUser                                        |                                                                                          |
| 5   | GetProfile                                               | Returns an [\#IProfile](#IProfile "wikilink").                                           |
| 6   | GetProfileDigest                                         |                                                                                          |
| 50  | IsUserRegistrationRequestPermitted                       |                                                                                          |
| 51  | TrySelectUserWithoutInteraction                          |                                                                                          |
| 100 | GetUserRegistrationNotifier                              | Returns an [\#INotifier](#INotifier "wikilink").                                         |
| 101 | GetUserStateChangeNotifier                               | Returns an [\#INotifier](#INotifier "wikilink").                                         |
| 102 | GetBaasAccountManagerForSystemService                    | Returns an [\#IManagerForSystemService](#IManagerForSystemService "wikilink").           |
| 103 | GetBaasUserAvailabilityChangeNotifier                    | Returns an [\#INotifier](#INotifier "wikilink").                                         |
| 104 | GetProfileUpdateNotifier                                 | Returns an [\#INotifier](#INotifier "wikilink").                                         |
| 110 | StoreSaveDataThumbnail                                   |                                                                                          |
| 111 | ClearSaveDataThumbnail                                   |                                                                                          |
| 112 | LoadSaveDataThumbnail                                    |                                                                                          |
| 190 | GetUserLastOpenedApplication                             |                                                                                          |
| 200 | BeginUserRegistration                                    |                                                                                          |
| 201 | CompleteUserRegistration                                 |                                                                                          |
| 202 | CancelUserRegistration                                   |                                                                                          |
| 203 | DeleteUser                                               |                                                                                          |
| 204 | SetUserPosition                                          |                                                                                          |
| 205 | GetProfileEditor                                         | Returns an [\#IProfileEditor](#IProfileEditor "wikilink").                               |
| 206 | CompleteUserRegistrationForcibly                         |                                                                                          |
| 210 | CreateFloatingRegistrationRequest                        | Returns an [\#IFloatingRegistrationRequest](#IFloatingRegistrationRequest "wikilink").   |
| 230 | AuthenticateServiceAsync                                 | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                 |
| 250 | GetBaasAccountAdministrator                              | Returns an [\#IAdministrator](#IAdministrator "wikilink").                               |
| 290 | ProxyProcedureForGuestLoginWithNintendoAccount           | Returns an [\#IOAuthProcedureForExternalNsa](#IOAuthProcedureForExternalNsa "wikilink"). |
| 291 | ProxyProcedureForFloatingRegistrationWithNintendoAccount | Returns an [\#IOAuthProcedureForExternalNsa](#IOAuthProcedureForExternalNsa "wikilink"). |
| 299 | SuspendBackgroundDaemon                                  | Returns an [\#ISessionObject](#ISessionObject "wikilink").                               |
| 997 | DebugInvalidateTokenCacheForUser                         |                                                                                          |
| 998 | DebugSetUserStateClose                                   |                                                                                          |
| 999 | DebugSetUserStateOpen                                    |                                                                                          |

## IManagerForSystemService

| Cmd | Name                                                         | Notes                                                                    |
| --- | ------------------------------------------------------------ | ------------------------------------------------------------------------ |
| 0   | CheckAvailability                                            |                                                                          |
| 1   | GetAccountId                                                 |                                                                          |
| 2   | EnsureIdTokenCacheAsync                                      | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                 |
| 3   | LoadIdTokenCache                                             |                                                                          |
| 100 | SetSystemProgramIdentification                               |                                                                          |
| 120 | GetNintendoAccountId                                         |                                                                          |
| 130 | GetNintendoAccountUserResourceCache                          |                                                                          |
| 131 | RefreshNintendoAccountUserResourceCacheAsync                 | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                 |
| 132 | RefreshNintendoAccountUserResourceCacheAsyncIfSecondsElapsed | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                 |
| 150 | CreateAuthorizationRequest                                   | Returns an [\#IAuthorizationRequest](#IAuthorizationRequest "wikilink"). |

## IFloatingRegistrationRequest

| Cmd | Name                           | Notes                                                    |
| --- | ------------------------------ | -------------------------------------------------------- |
| 0   | GetSessionId                   |                                                          |
| 12  | GetAccountId                   |                                                          |
| 13  | GetLinkedNintendoAccountId     |                                                          |
| 14  | GetNickname                    |                                                          |
| 15  | GetProfileImage                |                                                          |
| 21  | LoadIdTokenCache               |                                                          |
| 100 | RegisterAsync                  | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 101 | RegisterWithUidAsync           | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 110 | SetSystemProgramIdentification |                                                          |
| 111 | EnsureIdTokenCacheAsync        | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |

## IAdministrator

| Cmd | Name                                                              | Notes                                                                                                          |
| --- | ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| 0   | CheckAvailability                                                 |                                                                                                                |
| 1   | GetAccountId                                                      |                                                                                                                |
| 2   | EnsureIdTokenCacheAsync                                           | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 3   | LoadIdTokenCache                                                  |                                                                                                                |
| 100 | SetSystemProgramIdentification                                    |                                                                                                                |
| 120 | GetNintendoAccountId                                              |                                                                                                                |
| 130 | GetNintendoAccountUserResourceCache                               |                                                                                                                |
| 131 | RefreshNintendoAccountUserResourceCacheAsync                      | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 132 | RefreshNintendoAccountUserResourceCacheAsyncIfSecondsElapsed      | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 150 | CreateAuthorizationRequest                                        | Returns an [\#IAuthorizationRequest](#IAuthorizationRequest "wikilink").                                       |
| 200 | IsRegistered                                                      |                                                                                                                |
| 201 | RegisterAsync                                                     | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 202 | UnregisterAsync                                                   | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 203 | DeleteRegistrationInfoLocally                                     |                                                                                                                |
| 220 | SynchronizeProfileAsync                                           | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 221 | UploadProfileAsync                                                | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 222 | SynchronizeProfileAsyncIfSecondsElapsed                           | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 250 | IsLinkedWithNintendoAccount                                       |                                                                                                                |
| 251 | CreateProcedureToLinkWithNintendoAccount                          | Returns an [\#IOAuthProcedureForNintendoAccountLinkage](#IOAuthProcedureForNintendoAccountLinkage "wikilink"). |
| 252 | ResumeProcedureToLinkWithNintendoAccount                          | Returns an [\#IOAuthProcedureForNintendoAccountLinkage](#IOAuthProcedureForNintendoAccountLinkage "wikilink"). |
| 255 | CreateProcedureToUpdateLinkageStateOfNintendoAccount              | Returns an [\#IOAuthProcedure](#IOAuthProcedure "wikilink").                                                   |
| 256 | ResumeProcedureToUpdateLinkageStateOfNintendoAccount              | Returns an [\#IOAuthProcedure](#IOAuthProcedure "wikilink").                                                   |
| 260 | CreateProcedureToLinkNnidWithNintendoAccount                      | Returns an [\#IOAuthProcedure](#IOAuthProcedure "wikilink").                                                   |
| 261 | ResumeProcedureToLinkNnidWithNintendoAccount                      | Returns an [\#IOAuthProcedure](#IOAuthProcedure "wikilink").                                                   |
| 280 | ProxyProcedureToAcquireApplicationAuthorizationForNintendoAccount | Returns an [\#IOAuthProcedure](#IOAuthProcedure "wikilink").                                                   |
| 997 | DebugUnlinkNintendoAccountAsync                                   | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                                                       |
| 998 | DebugSetAvailabilityErrorDetail                                   |                                                                                                                |

## IAuthorizationRequest

| Cmd | Name                          | Notes                                                    |
| --- | ----------------------------- | -------------------------------------------------------- |
| 0   | GetSessionId                  |                                                          |
| 10  | InvokeWithoutInteractionAsync | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 19  | IsAuthorized                  |                                                          |
| 20  | GetAuthorizationCode          |                                                          |
| 21  | GetIdToken                    |                                                          |
| 22  | GetState                      |                                                          |

## IOAuthProcedure

| Cmd | Name               | Notes                                                    |
| --- | ------------------ | -------------------------------------------------------- |
| 0   | PrepareAsync       | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 1   | GetRequest         |                                                          |
| 2   | ApplyResponse      |                                                          |
| 3   | ApplyResponseAsync | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 10  | Suspend            |                                                          |

## IOAuthProcedureForExternalNsa

| Cmd | Name                       | Notes                                                    |
| --- | -------------------------- | -------------------------------------------------------- |
| 0   | PrepareAsync               | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 1   | GetRequest                 |                                                          |
| 2   | ApplyResponse              |                                                          |
| 3   | ApplyResponseAsync         | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 10  | Suspend                    |                                                          |
| 100 | GetAccountId               |                                                          |
| 101 | GetLinkedNintendoAccountId |                                                          |
| 102 | GetNickname                |                                                          |
| 103 | GetProfileImage            |                                                          |

## IOAuthProcedureForNintendoAccountLinkage

| Cmd | Name                                   | Notes                                                    |
| --- | -------------------------------------- | -------------------------------------------------------- |
| 0   | PrepareAsync                           | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 1   | GetRequest                             |                                                          |
| 2   | ApplyResponse                          |                                                          |
| 3   | ApplyResponseAsync                     | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 10  | Suspend                                |                                                          |
| 100 | GetRequestWithTheme                    |                                                          |
| 101 | IsNetworkServiceAccountReplaced        |                                                          |
| 199 | GetUrlForIntroductionOfExtraMembership |                                                          |

## INotifier

| Cmd | Name           |
| --- | -------------- |
| 0   | GetSystemEvent |

## IProfile

| Cmd | Name         |
| --- | ------------ |
| 0   | Get          |
| 1   | GetBase      |
| 10  | GetImageSize |
| 11  | LoadImage    |

## IProfileEditor

| Cmd | Name           |
| --- | -------------- |
| 0   | Get            |
| 1   | GetBase        |
| 10  | GetImageSize   |
| 11  | LoadImage      |
| 100 | Store          |
| 101 | StoreWithImage |

## IAsyncContext

| Cmd | Name           |
| --- | -------------- |
| 0   | GetSystemEvent |
| 1   | Cancel         |
| 2   | HasDone        |
| 3   | GetResult      |

## ISessionObject

| Cmd | Name  |
| --- | ----- |
| 999 | Dummy |

# acc:u0

This is
"nn::account::IAccountServiceForApplication".

| Cmd | Name                                | Notes                                                                      |
| --- | ----------------------------------- | -------------------------------------------------------------------------- |
| 0   | GetUserCount                        |                                                                            |
| 1   | GetUserExistence                    |                                                                            |
| 2   | ListAllUsers                        |                                                                            |
| 3   | ListOpenUsers                       |                                                                            |
| 4   | GetLastOpenedUser                   |                                                                            |
| 5   | GetProfile                          | Returns an [\#IProfile](#IProfile "wikilink").                             |
| 6   | GetProfileDigest                    |                                                                            |
| 50  | IsUserRegistrationRequestPermitted  |                                                                            |
| 51  | TrySelectUserWithoutInteraction     |                                                                            |
| 100 | InitializeApplicationInfo           |                                                                            |
| 101 | GetBaasAccountManagerForApplication | Returns an [\#IManagerForApplication](#IManagerForApplication "wikilink"). |
| 102 | AuthenticateApplicationAsync        | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                   |
| 110 | StoreSaveDataThumbnail              |                                                                            |
| 111 | ClearSaveDataThumbnail              |                                                                            |
| 120 | CreateGuestLoginRequest             | Returns an [\#IGuestLoginRequest](#IGuestLoginRequest "wikilink").         |

## IGuestLoginRequest

| Cmd | Name                       |
| --- | -------------------------- |
| 0   | GetSessionId               |
| 12  | GetAccountId               |
| 13  | GetLinkedNintendoAccountId |
| 14  | GetNickname                |
| 15  | GetProfileImage            |
| 21  | LoadIdTokenCache           |

## IManagerForApplication

| Cmd | Name                                              | Notes                                                                    |
| --- | ------------------------------------------------- | ------------------------------------------------------------------------ |
| 0   | CheckAvailability                                 |                                                                          |
| 1   | GetAccountId                                      |                                                                          |
| 2   | EnsureIdTokenCacheAsync                           | Returns an [\#IAsyncContext](#IAsyncContext "wikilink").                 |
| 3   | LoadIdTokenCache                                  |                                                                          |
| 130 | GetNintendoAccountUserResourceCacheForApplication |                                                                          |
| 150 | CreateAuthorizationRequest                        | Returns an [\#IAuthorizationRequest](#IAuthorizationRequest "wikilink"). |

# acc:u1

This is
"nn::account::IAccountServiceForSystemService".

| Cmd | Name                                  | Notes                                                                          |
| --- | ------------------------------------- | ------------------------------------------------------------------------------ |
| 0   | GetUserCount                          |                                                                                |
| 1   | GetUserExistence                      |                                                                                |
| 2   | ListAllUsers                          |                                                                                |
| 3   | ListOpenUsers                         |                                                                                |
| 4   | GetLastOpenedUser                     |                                                                                |
| 5   | GetProfile                            | Returns an [\#IProfile](#IProfile "wikilink").                                 |
| 6   | GetProfileDigest                      |                                                                                |
| 50  | IsUserRegistrationRequestPermitted    |                                                                                |
| 51  | TrySelectUserWithoutInteraction       |                                                                                |
| 100 | GetUserRegistrationNotifier           | Returns an [\#INotifier](#INotifier "wikilink").                               |
| 101 | GetUserStateChangeNotifier            | Returns an [\#INotifier](#INotifier "wikilink").                               |
| 102 | GetBaasAccountManagerForSystemService | Returns an [\#IManagerForSystemService](#IManagerForSystemService "wikilink"). |
| 103 | GetBaasUserAvailabilityChangeNotifier | Returns an [\#INotifier](#INotifier "wikilink").                               |
| 104 | GetProfileUpdateNotifier              | Returns an [\#INotifier](#INotifier "wikilink").                               |
| 110 | StoreSaveDataThumbnail                |                                                                                |
| 111 | ClearSaveDataThumbnail                |                                                                                |
| 112 | LoadSaveDataThumbnail                 |                                                                                |
| 190 | GetUserLastOpenedApplication          |                                                                                |
| 997 | DebugInvalidateTokenCacheForUser      |                                                                                |
| 998 | DebugSetUserStateClose                |                                                                                |
| 999 | DebugSetUserStateOpen                 |                                                                                |

# acc:aa

This is
"nn::account::IBaasAccessTokenAccessor".

| Cmd | Name                             | Notes                                                    |
| --- | -------------------------------- | -------------------------------------------------------- |
| 0   | EnsureCacheAsync                 | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 1   | LoadCache                        |                                                          |
| 2   | GetDeviceAccountId               |                                                          |
| 50  | RegisterNotificationTokenAsync   | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
| 51  | UnregisterNotificationTokenAsync | Returns an [\#IAsyncContext](#IAsyncContext "wikilink"). |
