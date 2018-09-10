# WIP, please ignore


#### To use this list, press Ctrl-F (or Cmd-F on Mac) and then type in the error code from yuzu. This should look similar to `XXXX-XXXX` where the Xs represent numbers and letters.

| Error Code | Description |
| -- | --|
| 0008-0000 | `Success` |
| 0008-0001 | `ErrorAlreadyLoaded` <br> This is an internal error and should be reported to the devs immediately. |
| 0008-0002 | `ErrorNotImplemented` |
| 0008-0003 | `ErrorNotInitialized` |
| 0008-0004 | `ErrorBadNPDMHeader` |
| 0008-0005 | `ErrorBadACIDHeader` |
| 0008-0006 | `ErrorBadACIHeader` |
| 0008-0007 | `ErrorBadFileAccessControl` |
| 0008-0008 | `ErrorBadFileAccessHeader` |
| 0008-0009 | `ErrorBadPFSHeader` |
| 0008-000A | `ErrorIncorrectPFSFileSize` |
| 0008-000B | `ErrorMissingHeaderKey` <br> To read any encrypted file, you need the NCA header key. This should go in your prod.keys under `header_key` |
| 0008-000C | `ErrorIncorrectHeaderKey` |
| 0008-000D | `ErrorNCA2` <br> The NCA you are attempting to load is using an older format that is not currently supported. If you would like support to be added, consider filing an issue. |
| 0008-000E | `ErrorNCA0` <br> The NCA you are attempting to load is using an older format that is not currently supported. If you would like support to be added, consider filing an issue. |
| 0008-000F | `ErrorMissingTitlekey` |
| 0008-0010 | `ErrorMissingTitlekek` |
| 0008-0001 | `ErrorInvalidRightsID` |
| 0008-0000 | `ErrorMissingKeyAreaKey` |
| 0008-0000 | `ErrorIncorrectKeyAreaKey` |
| 0008-0000 | `ErrorIncorrectTitlekeyOrTitlekek` |
| 0008-0000 | `ErrorXCIMissingProgramNCA` |
| 0008-0000 | `ErrorNCANotProgram` |
| 0008-0000 | `ErrorNoExeFS` |
| 0008-0000 | `ErrorBadXCIHeader` |
| 0008-0000 | `ErrorXCIMissingPartition` |
| 0008-0000 | `ErrorNullFile` |
| 0008-0000 | `ErrorMissingNPDM` |
| 0008-0000 | `Error32BitISA` <br> The game you are trying to run uses the 32-bit ARM architecture, which is not currently supported by yuzu. |
| 0008-0000 | `ErrorNoRomFS` |
| 0008-0000 | `ErrorIncorrectELFFileSize` |
| 0008-0000 | `ErrorLoadingNRO` |
| 0008-0000 | `ErrorNoIcon` |
| 0008-0000 | `ErrorNoControl` |
| 0008-0000 | `ErrorBadNAXHeader` |
| 0008-0000 | `ErrorIncorrectNAXFileSize` |
| 0008-0000 | `ErrorNAXKeyHMACFailed` |
| 0008-0000 | `ErrorNAXValidationHMACFailed` |
| 0008-0000 | `ErrorNAXKeyDerivationFailed` |
| 0008-0000 | `ErrorNAXInconvertibleToNCA` |
| 0008-0000 | `ErrorBadNAXFilePath` |
| 0008-0000 | `ErrorMissingSDSeed` |
| 0008-0000 | `ErrorMissingSDKEKSource` |
| 0008-0000 | `ErrorMissingAESKEKGenerationSource` |
| 0008-0000 | `ErrorMissingAESKeyGenerationSource` |
| 0008-0000 | `ErrorMissingSDSaveKeySource` |
| 0008-0000 | `ErrorMissingSDNCAKeySource` |
| 0008-0000 | `ErrorNSPMissingProgramNCA` |
| 0008-0000 | `ErrorBadBKTRHeader` |
| 0008-0000 | `ErrorBKTRSubsectionNotAfterRelocation` |
| 0008-0000 | `ErrorBKTRSubsectionNotAtEnd` |
| 0008-0000 | `ErrorBadRelocationBlock` |
| 0008-0000 | `ErrorBadSubsectionBlock` |
| 0008-0000 | `ErrorBadRelocationBuckets` |
| 0008-0000 | `ErrorBadSubsectionBuckets` |
| 0008-0000 | `ErrorMissingBKTRBaseRomFS` |