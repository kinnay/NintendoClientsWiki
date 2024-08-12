[Switch](Server-List#switch) > eShop Applet
---

The eShop is a website. When the eShop applet is opened, it visits https://bugyo.hac.lp1.eshop.nintendo.net/ashigaru/. The SwitchShop client certificate is required to access this website.

The eShop exposes system functions under the `window.nx` object.

The following objects are defined:

* `window.nx.canHistoryBack`
* `window.nx.footer.setDefaultAssign`
* `window.nx.footer.setAssign`
* `window.nx.footer.unsetAssign`
* `window.nx.isKeyboardShown`
* `window.nx.open1ButtonDialog`
* `window.nx.open2ButtonDialog`
* `window.nx.playSystemSe`
* `window.nx.setKeyboardChangedCallback`
* `window.nx.shop.canJumpToLhubApplet`
* `window.nx.shop.cancelAsync`
* `window.nx.shop.cancelDeviceAuthToken`
* `window.nx.shop.cancelNaAuthToken`
* `window.nx.shop.cancelSyncRights`
* `window.nx.shop.clearNaAuthTokenCache`
* `window.nx.shop.fadeOutStartAnimation`
* `window.nx.shop.getApplicationContentMetaStatusArray`
* `window.nx.shop.getDeviceAccountInfo`
* `window.nx.shop.getTotalSizeNand`
* `window.nx.shop.getTotalSizeSd`
* `window.nx.shop.isAnyApplicationRunning`
* `window.nx.shop.news.getSubscriptionStatus`
* `window.nx.shop.news.setSubscriptionStatus`
* `window.nx.shop.prepareSpaceSizes`
* `window.nx.shop.requestCleanupAllPreInstalledApplications`
* `window.nx.shop.requestDeviceRegistrationInfo`
* `window.nx.shop.requestDownloadTaskListOnEnd`
* `window.nx.shop.requestEdgeToken`
* `window.nx.shop.requestLinkDevice`
* `window.nx.shop.requestNaAuthToken`
* `window.nx.shop.requestRegisterDeviceAccount`
* `window.nx.shop.requestSyncRegistration`
* `window.nx.shop.requestSyncRights`
* `window.nx.shop.requestUnlinkDevice`
* `window.nx.shop.requestUnregisterDeviceAccount`
* `window.nx.shop.setDeviceAuthTokenAvailableCallback`
* `window.nx.shop.setKeyboardUserDictionary`
* `window.nx.shop.setNaAuthTokenAvailableCallback`
* `window.nx.system.getAccountNickname`
* `window.nx.system.isUserOperationLocked`
* `window.nx.system.loadAccountProfileImage`
* `window.nx.system.lockUserOperation`
* `window.nx.system.makeErrorCode`
* `window.nx.system.productModel`
* `window.nx.system.showError`
* `window.nx.system.version.comparable`

If the `window.nx` object is undefined, the eShop provides alternative behavior. For example, it will use `alert` to show an error dialog.