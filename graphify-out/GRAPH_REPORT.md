# Graph Report - BizCatchup  (2026-09-30)

## Corpus Check
- cluster-only mode — file stats not available

## Summary
- 4923 nodes · 9419 edges · 207 communities (157 shown, 50 thin omitted)
- Extraction: 99% EXTRACTED · 1% INFERRED · 0% AMBIGUOUS · INFERRED: 67 edges (avg confidence: 0.85)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- Community 0
- Community 1
- Community 2
- Community 3
- Community 4
- Community 5
- Community 6
- Community 7
- Community 8
- Community 9
- Community 10
- Community 11
- Community 12
- Community 13
- Community 14
- Community 15
- Community 16
- Community 17
- Community 18
- Community 19
- Community 20
- Community 21
- Community 22
- Community 23
- Community 24
- Community 25
- Community 26
- Community 27
- Community 28
- Community 29
- Community 30
- Community 31
- Community 32
- Community 33
- Community 34
- Community 35
- Community 36
- Community 37
- Community 38
- Community 39
- Community 40
- Community 41
- Community 42
- Community 43
- Community 44
- Community 45
- Community 46
- Community 47
- Community 48
- Community 49
- Community 50
- Community 51
- Community 52
- Community 53
- Community 54
- Community 55
- Community 56
- Community 57
- Community 58
- Community 59
- Community 60
- Community 61
- Community 62
- Community 63
- Community 64
- Community 65
- Community 66
- Community 67
- Community 68
- Community 69
- Community 70
- Community 71
- Community 72
- Community 73
- Community 74
- Community 75
- Community 76
- Community 77
- Community 78
- Community 79
- Community 80
- Community 81
- Community 82
- Community 83
- Community 84
- Community 85
- Community 86
- Community 87
- Community 88
- Community 89
- Community 90
- Community 91
- Community 92
- Community 93
- Community 94
- Community 95
- Community 96
- Community 97
- Community 98
- Community 99
- Community 100
- Community 101
- Community 102
- Community 103
- Community 104
- Community 105
- Community 106
- Community 107
- Community 108
- Community 109
- Community 110
- Community 111
- Community 112
- Community 113
- Community 114
- Community 115
- Community 116
- Community 117
- Community 118
- Community 119
- Community 120
- Community 121
- Community 122
- Community 123
- Community 124
- Community 125
- Community 126
- Community 127
- Community 128
- Community 129
- Community 130
- Community 131
- Community 132
- Community 133
- Community 134
- Community 135
- Community 136
- Community 137
- Community 138
- Community 139
- Community 140
- Community 142
- Community 143
- Community 144
- Community 145
- Community 146
- Community 147
- Community 148
- Community 149
- Community 150
- Community 151
- Community 152
- Community 153
- Community 154
- Community 155
- Community 156
- Community 157
- Community 158
- Community 159
- Community 160
- Community 161
- Community 162
- Community 163
- Community 164
- Community 165
- Community 166
- Community 167
- Community 168
- Community 169
- Community 170
- Community 171
- Community 172
- Community 173
- Community 174
- Community 175
- Community 176
- Community 177
- Community 179
- Community 181
- Community 182
- Community 183
- Community 184
- Community 185
- Community 186
- Community 187

## God Nodes (most connected - your core abstractions)
1. `github.com/NookPay/mould` - 134 edges
2. `Pipeline` - 108 edges
3. `Logger` - 77 edges
4. `GetPipeline()` - 75 edges
5. `Config` - 58 edges
6. `ERR_GIN_400()` - 58 edges
7. `NewDBHelper()` - 54 edges
8. `ExtractClaims()` - 43 edges
9. `BusinessCard` - 38 edges
10. `DBHelper` - 38 edges

## Surprising Connections (you probably didn't know these)
- `Load()` --calls--> `setDefaultConfig()`  [INFERRED]
  scanner/config/loader.go → scanner/config/default.go
- `ScanBusinessCardV2()` --calls--> `FetchMissingValuesFromGenAI()`  [INFERRED]
  scanner/pkg/endpoints/businesscards/scanV2.go → scanner/pkg/endpoints/businesscards/scan.go
- `ExtractColumnFromFile()` --calls--> `GetFileType()`  [EXTRACTED]
  scanner/pkg/endpoints/businesscards/scan.go → scanner/pkg/utils/utils.go
- `BulkCreateOrUpdateContacts()` --calls--> `GetOAuthProvider()`  [INFERRED]
  scanner/pkg/endpoints/integrations/contacts.go → scanner/pkg/endpoints/integrations/common.go
- `CreateOrUpdateContacts()` --calls--> `GetOAuthProvider()`  [INFERRED]
  scanner/pkg/endpoints/integrations/contacts.go → scanner/pkg/endpoints/integrations/common.go

## Import Cycles
- None detected.

## Communities (207 total, 50 thin omitted)

### Community 1 - "Community 1"
Cohesion: 0.01
Nodes (121): _animation, animationController, _applyDatasetState, bottomIndex, _buildAppBarTitle, _buildBodyForCurrentTab, _buildChoiceChip, _buildContactsTabBody (+113 more)

### Community 2 - "Community 2"
Cohesion: 0.09
Nodes (92): DuplicateFieldActionEnum, DuplicateFieldEnum, ExtractClaims(), health(), status(), versionedHello(), versionedHello(), GetPipeline() (+84 more)

### Community 3 - "Community 3"
Cohesion: 0.02
Nodes (90): actionButtons, ActionIconButton, addressController, allowMultiple, animatedIcon, baseColor, boxStyle, build (+82 more)

### Community 4 - "Community 4"
Cohesion: 0.02
Nodes (90): accordionBorder, addBoxTopBlue, AppColors, avatarPlaceholder, azureblue, black, blueWithOpacity, borderLight (+82 more)

### Community 5 - "Community 5"
Cohesion: 0.02
Nodes (75): actionButtons, ActionIconButton, addressController, allowMultiple, autofocus, build, buildDetailsTab, buildNotesTab (+67 more)

### Community 6 - "Community 6"
Cohesion: 0.03
Nodes (59): child, createState, details, didChangeAppLifecycleState, dispose, emailInputLabel, emailTakenErrorText, forgotPasswordButtonLabel (+51 more)

### Community 7 - "Community 7"
Cohesion: 0.11
Nodes (4): Operation, BusinessCardResponse, PlanType, TeamPlanRequest

### Community 8 - "Community 8"
Cohesion: 0.03
Nodes (68): _addField, _addNewField, build, _buildCards, _buildCategoryChips, _buildFields, _buildIntegrationCard, _buildShimmerCoverPhoto (+60 more)

### Community 9 - "Community 9"
Cohesion: 0.08
Nodes (11): FeedBack, RenameGroupPayload, RenameLabelPayload, GetFileType(), AcceptInviteOpsPayload, AcceptInvitePayload, ChangeOwnershipPayload, InviteTeamPayload (+3 more)

### Community 10 - "Community 10"
Cohesion: 0.05
Nodes (65): AnimatedStatus, _AnimatedStatusState, BusinessContactCreateView, _BusinessContactCreateViewState, BusinessScanDetailsView, _BusinessScanDetailsViewState, LoadingBusinessScanDetailsView, _LoadingBusinessScanDetailsViewState (+57 more)

### Community 11 - "Community 11"
Cohesion: 0.09
Nodes (44): react, CREATED_OPTIONS, CreatedFilter, createdRangeFor(), exportRowsToCsv(), ManageTeamsPage(), MEMBERS_OPTIONS, MembersFilter (+36 more)

### Community 12 - "Community 12"
Cohesion: 0.08
Nodes (45): run(), AppleWalletConfig, AzureConfig, DBConfig, setDefaultConfig(), FireBaseConfig, Load(), Config (+37 more)

### Community 13 - "Community 13"
Cohesion: 0.04
Nodes (48): build, createState, emailController, emails, _parseErrorMessage, role, teamId, build (+40 more)

### Community 14 - "Community 14"
Cohesion: 0.04
Nodes (38): _isListView, _preferences, showIsListViewCardList, build, count, createState, initState, integrationOptions (+30 more)

### Community 15 - "Community 15"
Cohesion: 0.05
Nodes (40): buildDetailsTab, CardHelper, build, businessCardGroups, cardHelper, createState, dispose, GroupScreen (+32 more)

### Community 16 - "Community 16"
Cohesion: 0.04
Nodes (48): ContactsScopeToggleBar, TextDetailWidget, RoundTile, ShimmerBusinessScanDetailsView, SquareTile, SquareTileStats, TextDetailWidget, build (+40 more)

### Community 17 - "Community 17"
Cohesion: 0.04
Nodes (50): acceptInvite, addBusinessCard, addBusinessCardManually, addDigitalBusinessCard, addDigitalCardLeadContact, API, bizScanBaseURL, bulkAssociateGroupLabels (+42 more)

### Community 18 - "Community 18"
Cohesion: 0.14
Nodes (16): DuplicateConfig, LeadContact, ScanBusinessCardV2Request, BulkCreateOrUpdateContactsPayload, Progress, DefaultScanBusinessCardPayload(), plainTextHasTrailingNewline(), PlainTextToQuill() (+8 more)

### Community 19 - "Community 19"
Cohesion: 0.04
Nodes (39): allowRequest, androidPlatformChannelSpecifics, body, cancel, cancelNotification, _dedupedPermissionCheck, details, existing (+31 more)

### Community 20 - "Community 20"
Cohesion: 0.04
Nodes (47): backgroundColor, badgeImageUrl, BusinessCardImage, cardDescription, cardTitle, companyName, connectFields, ContactForm (+39 more)

### Community 21 - "Community 21"
Cohesion: 0.05
Nodes (37): createDigitalBusinessCard, deleteDigitalBusinessCard, DigitalBusinessCardService, fetchCardBySharableLink, getAutoDescription, getDigitalBusinessCard, getDigitalBusinessCards, getTeamCards (+29 more)

### Community 22 - "Community 22"
Cohesion: 0.06
Nodes (11): InMemoryCache[T], getConfig(), NewInMemoryCache(), Cache, HumanizeDuration(), NewPasskitGenerator(), CleanupManager, Manager (+3 more)

### Community 23 - "Community 23"
Cohesion: 0.05
Nodes (14): fl_register_plugins(), main(), my_application_activate(), my_application_class_init(), my_application_dispose(), my_application_init(), my_application_local_command_line(), my_application_new() (+6 more)

### Community 24 - "Community 24"
Cohesion: 0.06
Nodes (29): showActionDialog, AddCardBox, build, height, onTap, width, animationController, build (+21 more)

### Community 25 - "Community 25"
Cohesion: 0.06
Nodes (39): build, getCardListView, getCompletedCardListView, HotelHomeScreen, _HotelHomeScreenState, onBarCodeScan, _showInProgressFilter, LabelCountNotifier (+31 more)

### Community 26 - "Community 26"
Cohesion: 0.04
Nodes (42): _accent, _allPlans, _annual, annualPrice, build, _contactUs, createState, enabled (+34 more)

### Community 27 - "Community 27"
Cohesion: 0.08
Nodes (6): BulkAssociateGroupOrLabelPayload, DBHelper, Filter, QueryPayload, Remove(), ToCamelCase()

### Community 28 - "Community 28"
Cohesion: 0.08
Nodes (21): nextConfig, next, AdminLayout(), accountsLinks, AppSidebar(), AppTopbar(), SidebarContext, SidebarContextValue (+13 more)

### Community 29 - "Community 29"
Cohesion: 0.05
Nodes (42): Address, addressMap, businessCard, canRescan, city, companyLogsURL, companyName, contactName (+34 more)

### Community 30 - "Community 30"
Cohesion: 0.05
Nodes (31): fetchScanLimits, fetchTeamScanData, fetchUserScanData, _firestore, ScanService, updateTeamScanData, updateUserScanData, build (+23 more)

### Community 31 - "Community 31"
Cohesion: 0.05
Nodes (34): _awaitIdentify, _cached, cachedTier, changePlan, currentTier, expiresAt, _fromCustomerInfo, hasPremium (+26 more)

### Community 32 - "Community 32"
Cohesion: 0.05
Nodes (32): dispose, _labelCountSubscription, _listenToLabels, _totalLabelCount, _appConfigSubscription, cancelListeners, _dailyScanned, _dailyScannedLimit (+24 more)

### Community 33 - "Community 33"
Cohesion: 0.09
Nodes (19): SanitizeBusinessCardQRPayload(), containsIgnoreCase(), ParserManager, isDomainMatch(), isLinkedInURL(), isSkypeURL(), isTelegramURL(), isWhatsAppURL() (+11 more)

### Community 34 - "Community 34"
Cohesion: 0.09
Nodes (31): firebase, handleSubmit(), listCards(), mockListCards(), ApiError, buildQueryString(), http(), RequestOptions (+23 more)

### Community 35 - "Community 35"
Cohesion: 0.05
Nodes (32): addBusinessCard, addBusinessCardManually, addLeadContact, applyFilters, BusinessCardService, createOrUpdateOauthProviderContacts, createRunHistory, defaultGroups (+24 more)

### Community 36 - "Community 36"
Cohesion: 0.05
Nodes (34): _BannerKind, borderColor, build, buttonColor, buttonLabel, createState, _dismissed, icon (+26 more)

### Community 37 - "Community 37"
Cohesion: 0.06
Nodes (26): animationController, build, WelcomeView, Workflow, addWorkflow, checkIfIntegrationCanBeDeleted, deleteWorkflow, fetchTotalWorkflowsCount (+18 more)

### Community 38 - "Community 38"
Cohesion: 0.06
Nodes (31): accomodationListData, allAccommodationUI, build, checkAppPosition, createState, distanceViewUI, distValue, filters (+23 more)

### Community 39 - "Community 39"
Cohesion: 0.06
Nodes (26): exportFileFormat, flexScheme, isDark, ModelTheme, _preferences, setExportFileFormat, setFlexScheme, setIsDark (+18 more)

### Community 40 - "Community 40"
Cohesion: 0.05
Nodes (32): build, _cancelStep, canShowIntegration, createState, createWorkflowLoading, _cronTime, _currentStep, dispose (+24 more)

### Community 41 - "Community 41"
Cohesion: 0.07
Nodes (31): eslintConfig, name, private, scripts, build, dev, lint, start (+23 more)

### Community 42 - "Community 42"
Cohesion: 0.12
Nodes (32): lucide-react, cardColumns, DashboardPage(), metric(), teamColumns, StatCard(), StatCardProps, getTeamById() (+24 more)

### Community 43 - "Community 43"
Cohesion: 0.06
Nodes (33): _addCardToWallet, _addToAppleWallet, _addToGoogleWallet, _appleWalletService, build, _buildActionButton, _buildCardPreview, _buildConnectFields (+25 more)

### Community 44 - "Community 44"
Cohesion: 0.12
Nodes (30): @faker-js/faker, getDashboardStats(), ListTeamsParams, blankish(), buildCard(), CARD_COUNT, getCardCountForTeam(), getMockCards() (+22 more)

### Community 45 - "Community 45"
Cohesion: 0.06
Nodes (27): _buildDigitalCardTile, _buildMyCardsSection, _buildTeamCardsSection, card, count, createState, currentPage, displayName (+19 more)

### Community 46 - "Community 46"
Cohesion: 0.13
Nodes (25): @base-ui/react, class-variance-authority, StatBlock(), TeamListCard(), TeamMembersList(), NotFound(), PaginationBarProps, TeamLimitsDialog() (+17 more)

### Community 47 - "Community 47"
Cohesion: 0.10
Nodes (16): DBHelper, FirebaseStorage, DBHelper, BaseDBHelper, NewBaseDBHelper(), NewDBHelper(), NewDBHelper(), NewDBHelper() (+8 more)

### Community 48 - "Community 48"
Cohesion: 0.06
Nodes (29): addContact, build, buildOptionTile, bytes, call, checkIfContactExists, ContactSelectionDialog, controllers (+21 more)

### Community 49 - "Community 49"
Cohesion: 0.06
Nodes (33): AppSizes, avatarLarge, avatarMedium, avatarSmall, bottomNavClearance, cardCoverHeight, carouselHeight, coverStackHeight (+25 more)

### Community 50 - "Community 50"
Cohesion: 0.07
Nodes (31): addedScopes, _authNotifier, _authNotifierListener, _authorize, build, createContact, createState, _currentStep (+23 more)

### Community 51 - "Community 51"
Cohesion: 0.06
Nodes (27): AnalyticsService, clearUserInfo, _ensureUserInfoSynced, firstName, initialize, initializeUninstallTracking, _isInitialized, lastName (+19 more)

### Community 52 - "Community 52"
Cohesion: 0.06
Nodes (23): authStateChangesStream, _authSubscription, build, _buildMenuTile, _buildProfileCard, createState, dispose, DrawerIndex (+15 more)

### Community 53 - "Community 53"
Cohesion: 0.06
Nodes (26): dailyLimit, defaultLimits, fromMap, lastScanDate, ScanLimits, scannedTodayCount, teamId, teamMemberLimit (+18 more)

### Community 54 - "Community 54"
Cohesion: 0.08
Nodes (6): Fields, logrusLogEntry, logrusLogger, zapLogger, convertToLogrusFields(), WithFields()

### Community 55 - "Community 55"
Cohesion: 0.07
Nodes (23): byFormat, CardOverlay, cornerRadius, orientation, OverlayFormat, OverlayModel, OverlayOrientation, ratio (+15 more)

### Community 56 - "Community 56"
Cohesion: 0.07
Nodes (21): _addCardToWallet, _addToAppleWallet, _addToGoogleWallet, _appleWalletService, build, buildSectionHeader, buildShareOption, buildShareOptionCard (+13 more)

### Community 57 - "Community 57"
Cohesion: 0.07
Nodes (25): CONTACT_DISCLOSURE_SHOWN, deleteContact, EXPORT_FILE_FORMAT, getContactDisclosureShown, getContactID, getExportFileFormat, getIsListView, getPhoneContactAddWorkflow (+17 more)

### Community 58 - "Community 58"
Cohesion: 0.07
Nodes (29): code, createdAt, description, email, emails, fromJson, hasTeamAccess, id (+21 more)

### Community 59 - "Community 59"
Cohesion: 0.14
Nodes (24): revenueCatEvent, revenueCatWebhook, jobFamily, jobStep, Pipeline, anchorFor(), defaultAnchor(), findStep() (+16 more)

### Community 60 - "Community 60"
Cohesion: 0.07
Nodes (17): _buildTextTheme, buildTheme, getBaseTheme, HotelAppTheme, myCustomScheme, build, _buildComposer, createState (+9 more)

### Community 61 - "Community 61"
Cohesion: 0.07
Nodes (19): appUrlGuide, baseUrl, category, fullUrlGuide, getIntegrations, hintText, icon, Integration (+11 more)

### Community 62 - "Community 62"
Cohesion: 0.14
Nodes (8): Workflow, ArrContains(), Contains(), ContainsAny(), StructToMap(), WorkflowFilter, Email, Zoho

### Community 63 - "Community 63"
Cohesion: 0.08
Nodes (21): _barcode, build, _cameraController, createState, _detectedData, dispose, _finishScanning, _handleBarcode (+13 more)

### Community 64 - "Community 64"
Cohesion: 0.07
Nodes (23): AppTheme, body1, body2, caption, chipBackground, dark_grey, darkerText, darkText (+15 more)

### Community 65 - "Community 65"
Cohesion: 0.08
Nodes (19): build, businessCard, _checkContact, ContactWidget, _ContactWidgetState, _createOrUpdateContact, createState, description (+11 more)

### Community 66 - "Community 66"
Cohesion: 0.08
Nodes (21): _appsflyerSdk, AppsFlyerService, initialize, _appsflyerSdk, AppsFlyerService, initialize, _isInitialized, logEvent (+13 more)

### Community 67 - "Community 67"
Cohesion: 0.07
Nodes (26): app_links, cloud_firestore, desktop_webview_auth, device_info_plus, file_picker, file_selector_macos, firebase_analytics, firebase_app_check (+18 more)

### Community 68 - "Community 68"
Cohesion: 0.08
Nodes (23): build, createState, _debounce, dispose, FilterBottomSheet, _FilterBottomSheetState, initialSelectedItems, initState (+15 more)

### Community 69 - "Community 69"
Cohesion: 0.08
Nodes (22): build, _buildEventButton, _buildTextField, createState, _currencyController, facebookAppEvents, _planNameController, _priceController (+14 more)

### Community 70 - "Community 70"
Cohesion: 0.07
Nodes (21): clearSession, _collectionName, _currentSessionToken, _currentUserId, didChangeAppLifecycleState, dispose, _getDeviceName, _getPlatform (+13 more)

### Community 71 - "Community 71"
Cohesion: 0.12
Nodes (5): ListAdminBusinessCardsResponse, BusinessCard, ContactProvider, GoogleContacts, HubSpot

### Community 73 - "Community 73"
Cohesion: 0.08
Nodes (19): build, _buildActionCircle, _buildGroupChip, _buildLabelChip, _buildOverflowChip, _buildTagRow, CompactBusinessCardItem, _estimateChipWidth (+11 more)

### Community 74 - "Community 74"
Cohesion: 0.08
Nodes (19): addedScopes, allColumns, build, columns, createState, CSVImportSetup, _CSVImportSetupState, _currentStep (+11 more)

### Community 75 - "Community 75"
Cohesion: 0.08
Nodes (22): APP_OPEN_EVENT_ID, ApptroveService, CARD_SUCCESS_EVENT_ID, ENV_DEVELOPMENT, ENV_PRODUCTION, ENV_TESTING, _getIDFA, initialize (+14 more)

### Community 76 - "Community 76"
Cohesion: 0.08
Nodes (23): 🚀 API v1.0 (`/v1.0`), 🚀 API v2.0 (`/v2.0`), Base URLs, 📇 Business Cards, 🛠️ DevOps & App Config, 📱 Digital Business Cards, 🌍 Global Routes, 🔗 Integrations & OAuth (+15 more)

### Community 77 - "Community 77"
Cohesion: 0.12
Nodes (10): AzureManager, EmailPayload, Zeptomail, Manager, NewLogoManager(), Requests, New(), GetRetriableClient() (+2 more)

### Community 79 - "Community 79"
Cohesion: 0.08
Nodes (25): dependencies, @base-ui/react, class-variance-authority, cn, date-fns, firebase, lucide-react, next (+17 more)

### Community 80 - "Community 80"
Cohesion: 0.08
Nodes (23): decrementGroupCount, decrementLabelCount, decrementTotalCardCount, decrementTotalGroupCardCount, decrementTotalLabelCardCount, _groupCount, incrementGroupCount, incrementLabelCount (+15 more)

### Community 81 - "Community 81"
Cohesion: 0.08
Nodes (22): build, createState, errorDescription, errorMessage, lottieFilePath, onComplete, WorkflowFailureCreatedScreen, build (+14 more)

### Community 82 - "Community 82"
Cohesion: 0.08
Nodes (13): build, canPop, changeIndex, createState, drawerIndex, _drawerWidth, getScreenView, iconAnimationController (+5 more)

### Community 83 - "Community 83"
Cohesion: 0.15
Nodes (23): Err, ERR_API_SRV_STR(), ERR_API_WEB_HOK(), ERR_ATT_PRX(), ERR_BIN_UPD(), ERR_DAT_CONN_DWN(), ERR_DAT_WS_RD(), ERR_DNS_RLV() (+15 more)

### Community 84 - "Community 84"
Cohesion: 0.09
Nodes (22): build, _buildContactAvatar, BulkCreateUpdateWidget, _BulkCreateUpdateWidgetState, createState, dispose, _errorContacts, extraData (+14 more)

### Community 85 - "Community 85"
Cohesion: 0.09
Nodes (17): build, createState, dispose, _handleTabChange, initialTabIndex, initState, _integrations, integrationsFutureOverride (+9 more)

### Community 86 - "Community 86"
Cohesion: 0.08
Nodes (20): APP_OPEN_EVENT_ID, ApptroveService, CARD_SUCCESS_EVENT_ID, ENV_DEVELOPMENT, ENV_PRODUCTION, ENV_TESTING, initialize, _isInitialized (+12 more)

### Community 87 - "Community 87"
Cohesion: 0.10
Nodes (10): createPassData(), generateSerialNumber(), validateWalletPassRequest(), GenerateSerialNumberFromCardID(), GenerateSerialNumberFromEmail(), DeleteWalletPassResponse, GenerateWalletPassRequest, GenerateWalletPassResponse (+2 more)

### Community 88 - "Community 88"
Cohesion: 0.09
Nodes (21): aliases, components, hooks, lib, ui, utils, iconLibrary, menuAccent (+13 more)

### Community 89 - "Community 89"
Cohesion: 0.13
Nodes (8): Address, ExtractEntityResponse, QRExtractEntityResponse, SocialProfiles, Gemini, NewGemini(), NewAIQRLinkParser(), NewParserManager()

### Community 90 - "Community 90"
Cohesion: 0.10
Nodes (17): _animation, _animationController, _auth, build, cancelVerification, canResendEmail, createState, dispose (+9 more)

### Community 91 - "Community 91"
Cohesion: 0.10
Nodes (13): build, createState, _currentPage, _downloadImage, flutterLocalNotificationsPlugin, FullSizeImageView, _FullSizeImageViewState, imageUrls (+5 more)

### Community 92 - "Community 92"
Cohesion: 0.10
Nodes (20): APP_OPEN_EVENT_ID, ApptroveService, CARD_SUCCESS_EVENT_ID, ENV_DEVELOPMENT, ENV_PRODUCTION, ENV_TESTING, initialize, _isInitialized (+12 more)

### Community 93 - "Community 93"
Cohesion: 0.10
Nodes (19): actions, ADD_CARD_WORKFLOW, createdAt, data, DELETE_CARD_WORKFLOW, event, Filters, fromJson (+11 more)

### Community 94 - "Community 94"
Cohesion: 0.10
Nodes (16): dispose, hasTeamAccess, initializeRealTimeUpdates, isPremium, _listeningTeamId, _onRevenueCatTierChanged, _plan, planLabel (+8 more)

### Community 95 - "Community 95"
Cohesion: 0.10
Nodes (16): body, build, _controller, createState, _dismiss, _dismissing, _dismissTimer, dispose (+8 more)

### Community 96 - "Community 96"
Cohesion: 0.11
Nodes (18): compilerOptions, allowJs, esModuleInterop, incremental, isolatedModules, jsx, lib, module (+10 more)

### Community 97 - "Community 97"
Cohesion: 0.11
Nodes (12): actions, appBar, AppProfileScreen, auth, build, children, createState, _deleteAccount (+4 more)

### Community 98 - "Community 98"
Cohesion: 0.11
Nodes (13): build, ComingSoonRadioListTile, enableFeedback, groupValue, onChanged, title, value, build (+5 more)

### Community 99 - "Community 99"
Cohesion: 0.11
Nodes (15): clearUserData, clearUserId, _facebookAppEvents, initialize, _isInitialized, logCardScanSuccess, logEvent, logLogin (+7 more)

### Community 100 - "Community 100"
Cohesion: 0.16
Nodes (12): Scale(), Create, Destroy, SetQuitOnClose, Show, UpdateTheme, Win32Window::Win32Window(), WindowClassRegistrar (+4 more)

### Community 101 - "Community 101"
Cohesion: 0.17
Nodes (13): ContactInfo, ImportContactPayload, QRScanBusinessCardPayload, ExtractColumnFromFile(), FetchMissingValuesFromGenAI(), guessEntityMapping(), isValidPhoneNumber(), readCSVColumns() (+5 more)

### Community 102 - "Community 102"
Cohesion: 0.11
Nodes (14): build, EmptyListView, entity, icon, imageAsset, message, searchQuery, subtitleStyle (+6 more)

### Community 103 - "Community 103"
Cohesion: 0.11
Nodes (15): DEFAULT_SORT_BY, DEFAULT_SORT_ORDER, Filters, groups, hashCode, hideGroup, hideLabel, isEmpty (+7 more)

### Community 104 - "Community 104"
Cohesion: 0.12
Nodes (15): build, convertRadiusToSigma, createState, CustomRangeThumbShape, _disabledThumbSize, getPreferredSize, initState, _leftTriangle (+7 more)

### Community 105 - "Community 105"
Cohesion: 0.12
Nodes (13): build, convertRadiusToSigma, createState, CustomThumbShape, _disabledThumbSize, distValue, getPreferredSize, initState (+5 more)

### Community 106 - "Community 106"
Cohesion: 0.12
Nodes (13): backgroundColor, build, CustomSwitch, onChanged, value, build, buttonStyle, buttonText (+5 more)

### Community 107 - "Community 107"
Cohesion: 0.11
Nodes (14): isAndroid, isEmailSupported, isFuchsia, isIOS, isLinux, isMacOS, isPhoneSupported, isSmsSupported (+6 more)

### Community 108 - "Community 108"
Cohesion: 0.14
Nodes (14): DBHelper, CancelFamilyJobs(), RescheduleInactivityJob(), ScheduleSignupJobs(), NewDBHelper(), NewDBHelper(), NewDBHelper(), containsInt64() (+6 more)

### Community 109 - "Community 109"
Cohesion: 0.15
Nodes (4): Integration, GetContactFromInterface(), Base, Slack

### Community 110 - "Community 110"
Cohesion: 0.23
Nodes (10): cn, DataTableCard(), DataTableCardProps, Skeleton(), Table(), TableBody(), TableCell(), TableHead() (+2 more)

### Community 111 - "Community 111"
Cohesion: 0.12
Nodes (16): _buildHeaderForCurrentTab, _buildScopedContactsHeader, getCompletedCardUIHeader, scanQRCode, showImportOptionsSheet, _showLimitReachedDialog, _openNoteEditorPage, _openNoteEditorPage (+8 more)

### Community 112 - "Community 112"
Cohesion: 0.17
Nodes (10): New(), Authentication(), JWTDecode(), WsValidator(), RegisterRoutes(), RegisterRoutes(), RegisterRoutes(), FirebaseAuthMiddleware (+2 more)

### Community 113 - "Community 113"
Cohesion: 0.13
Nodes (13): build, createState, entity, FilterBarUI, _FilterBarUIState, filterScreen, future, FutureBuilderText (+5 more)

### Community 114 - "Community 114"
Cohesion: 0.12
Nodes (13): _applySearchablePrefixFilter, BusinessGroupService, createOrUpdateGroups, createOrUpdateLabels, deleteGroup, deleteLabel, _directoryQuery, fixGroupCounts (+5 more)

### Community 115 - "Community 115"
Cohesion: 0.12
Nodes (10): downloadFileForWeb, anchor, blob, downloadFileForWeb, fileUrl, anchor, blob, bytes (+2 more)

### Community 116 - "Community 116"
Cohesion: 0.12
Nodes (10): build, child, maxWidth, ResponsiveConstrainedBox, android, DefaultFirebaseOptions, ios, macos (+2 more)

### Community 117 - "Community 117"
Cohesion: 0.12
Nodes (11): build, color, createState, iconData, _isLoading, build, icon, imageAsset (+3 more)

### Community 118 - "Community 118"
Cohesion: 0.13
Nodes (13): build, _buildOnboardingPage, createState, _currentPage, dispose, initState, IntroductionAnimationScreen, _IntroductionAnimationScreenState (+5 more)

### Community 119 - "Community 119"
Cohesion: 0.17
Nodes (13): OnCreate, OnDestroy, Point, x, y, Win32Window, child_content_, GetClientArea (+5 more)

### Community 120 - "Community 120"
Cohesion: 0.13
Nodes (13): build, _clearIconAnimationController, _clearSearch, createState, dispose, focusNode, initState, _onFocusChanged (+5 more)

### Community 121 - "Community 121"
Cohesion: 0.13
Nodes (13): BusinessCardID, CreatedAt, DataIn, DataOut, ErrorReason, fromJson, RunHistory, Status (+5 more)

### Community 122 - "Community 122"
Cohesion: 0.25
Nodes (9): BusinessCardImage, ContactForm, DBHelper, DigitalCardConnectFields, DigitalCardFieldValue, QRCodeSetting, SharableProperties, DigitalBusinessCard (+1 more)

### Community 123 - "Community 123"
Cohesion: 0.14
Nodes (12): BusinessCardGroup, count, DocumentID, fromJson, hashCode, name, operator, position (+4 more)

### Community 124 - "Community 124"
Cohesion: 0.14
Nodes (12): BusinessCardLabel, count, DocumentID, fromJson, hashCode, name, operator, position (+4 more)

### Community 125 - "Community 125"
Cohesion: 0.15
Nodes (13): detectDuplicates, DuplicateAction, DuplicateActionExtension, duplicateCardSettings, DuplicateFieldConfig, fromInt, fromMap, getShortHandDuplicateAction (+5 more)

### Community 126 - "Community 126"
Cohesion: 0.17
Nodes (11): build, createState, initState, isSelectedDateAdded, isSelectedDateUpdated, isSelectedName, isSortAscending, sortBy (+3 more)

### Community 127 - "Community 127"
Cohesion: 0.15
Nodes (7): DEFAULT_FLEX_SCHEME, GLOBAL, PRIVACY_POLICY_URL, SORT_BY_ASCENDING, SORT_BY_COLUMN, team, TERMS_AND_CONDITIONS_URL

### Community 128 - "Community 128"
Cohesion: 0.15
Nodes (12): companyName, contactName, email, fromJson, id, jobTitles, LeadContact, notes (+4 more)

### Community 129 - "Community 129"
Cohesion: 0.15
Nodes (11): csv, google, hubspot, IntegrationConstants, integrationIcons, integrationSteps, jira, salesforce (+3 more)

### Community 130 - "Community 130"
Cohesion: 0.17
Nodes (7): build, createState, initState, _load, NotificationSettingsScreen, _NotificationSettingsScreenState, _osGranted

### Community 131 - "Community 131"
Cohesion: 0.19
Nodes (4): wWinMain(), CreateAndAttachConsole(), GetCommandLineArguments(), Utf8FromUtf16()

### Community 132 - "Community 132"
Cohesion: 0.37
Nodes (11): Address, AnalyzeResult, BoundingRegion, Document, DocumentField, DocumentResponse, Line, Page (+3 more)

### Community 133 - "Community 133"
Cohesion: 0.32
Nodes (4): docID(), DBHelper, NotificationJob, GetTimeDiff()

### Community 135 - "Community 135"
Cohesion: 0.17
Nodes (11): appsFlyerAppIdIOS, appsFlyerDevKey, apptroveSdkTokenAndroid, apptroveSdkTokenIOS, apptroveSecretIdAndroid, apptroveSecretIdIOS, apptroveSecretKeyAndroid, apptroveSecretKeyIOS (+3 more)

### Community 136 - "Community 136"
Cohesion: 0.17
Nodes (11): 1. Onboarding & Authentication, 2. Creating a Digital Card, 3. Scanning a Business Card, 4. Customizing Settings, Basic Usage Guide, BizCatchUp, Features, Prerequisites (+3 more)

### Community 137 - "Community 137"
Cohesion: 0.20
Nodes (4): Team, createPDFFile(), StringArrContains(), TeamMember

### Community 138 - "Community 138"
Cohesion: 0.18
Nodes (9): AppDurations, debounce, extraSlow, fast, medium, normal, oneSecond, slow (+1 more)

### Community 139 - "Community 139"
Cohesion: 0.18
Nodes (10): background_color, description, display, icons, name, orientation, prefer_related_applications, short_name (+2 more)

### Community 143 - "Community 143"
Cohesion: 0.22
Nodes (5): bizcatchupApp, .body, ContentView, .body, SwiftUI

### Community 144 - "Community 144"
Cohesion: 0.20
Nodes (7): AirbridgeService, clearUser, _isEnabled, logEvent, setUserEmail, setUserId, setUserName

### Community 145 - "Community 145"
Cohesion: 0.36
Nodes (5): EnableFullDpiSupportIfAvailable(), GetHandle, GetThisFromHandle, MessageHandler, WndProc

### Community 146 - "Community 146"
Cohesion: 0.31
Nodes (9): PhoneNumberOutputType, createCSVFile(), createXLSXFile(), formatPhoneNumber(), getWorkPhones(), setColumnWidths(), QuillToPlainText(), GetFirstAndLastName() (+1 more)

### Community 147 - "Community 147"
Cohesion: 0.24
Nodes (7): getFormatter(), newLogrusLogger(), LoggingConfig, NewLogger(), getEncoder(), getZapLevel(), newZapLogger()

### Community 148 - "Community 148"
Cohesion: 0.36
Nodes (3): AppConfig, DBHelper, toInt64()

### Community 149 - "Community 149"
Cohesion: 0.25
Nodes (7): API wiring (`src/lib/api/*`), Auth, BizCatchup Super Admin, Getting started, Scripts, Status: wired to the real production backend, What's still mocked / unavailable

### Community 150 - "Community 150"
Cohesion: 0.25
Nodes (6): build, DeleteDialog, _deleteFuture, isSelectItem, onDelete, selectedItem

### Community 151 - "Community 151"
Cohesion: 0.25
Nodes (6): content, page, PageRequest, PageResponse, size, totalElements

### Community 152 - "Community 152"
Cohesion: 0.25
Nodes (6): androidSetupKey, iosSetupKey, proEntitlementID, RevenueCat, teamEntitlementID, testStoreApiKey

### Community 153 - "Community 153"
Cohesion: 0.25
Nodes (4): build, ContactDisclosureDialog, onAccept, onDecline

### Community 154 - "Community 154"
Cohesion: 0.25
Nodes (7): Attribution, Contributor Covenant Code of Conduct, Enforcement, Our Pledge, Our Responsibilities, Our Standards, Scope

### Community 155 - "Community 155"
Cohesion: 0.33
Nodes (5): FBSDKCoreKit, Flutter, flutter_local_notifications, UIKit, XCTest

### Community 156 - "Community 156"
Cohesion: 0.29
Nodes (5): accomodationList, isSelected, PopularFilterListData, popularFList, titleTxt

### Community 157 - "Community 157"
Cohesion: 0.33
Nodes (4): getTags(), recursivelySet(), TestNestedValues(), TestSimpleValues()

### Community 158 - "Community 158"
Cohesion: 0.43
Nodes (4): OAuthTokenResponse, DBHelper, OAuthApplication, fetchToken()

### Community 160 - "Community 160"
Cohesion: 0.33
Nodes (3): FlutterWindow, flutter_controller_, project_

### Community 161 - "Community 161"
Cohesion: 0.47
Nodes (3): RootCommand(), AttachCLIFlags(), main()

### Community 168 - "Community 168"
Cohesion: 0.40
Nodes (3): ScanLimit, TeamScan, MaxInt()

### Community 170 - "Community 170"
Cohesion: 0.50
Nodes (3): ContestTabHeader, ContestTabHeader, ContestTabHeader

### Community 171 - "Community 171"
Cohesion: 0.50
Nodes (3): Size, height, width

## Knowledge Gaps
- **2485 isolated node(s):** `build.sh script`, `LeadContact`, `ContactForm`, `Operation`, `AppVersionUpdateRequest` (+2480 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 3090 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **50 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Win32Window` connect `Community 119` to `Community 160`, `Community 100`, `Community 171`, `Community 140`, `Community 141`, `Community 145`?**
  _High betweenness centrality (0.026) - this node is a cross-community bridge._
- **Why does `OnCreate` connect `Community 119` to `Community 160`, `Community 140`, `Community 23`?**
  _High betweenness centrality (0.013) - this node is a cross-community bridge._
- **Why does `RegisterPlugins()` connect `Community 23` to `Community 119`?**
  _High betweenness centrality (0.012) - this node is a cross-community bridge._
- **What connects `build.sh script`, `LeadContact`, `ContactForm` to the rest of the system?**
  _2485 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Community 0` be split into smaller, more focused modules?**
  _Cohesion score 0.014814814814814815 - nodes in this community are weakly interconnected._
- **Should `Community 1` be split into smaller, more focused modules?**
  _Cohesion score 0.014925373134328358 - nodes in this community are weakly interconnected._
- **Should `Community 2` be split into smaller, more focused modules?**
  _Cohesion score 0.09105467856325783 - nodes in this community are weakly interconnected._