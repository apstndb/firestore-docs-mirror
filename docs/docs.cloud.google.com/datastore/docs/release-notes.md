This page documents production updates to Datastore. You can periodically check this page for announcements about new or updated features, bug fixes, known issues, and deprecated functionality.

You can see the latest product updates for all of Google Cloud on the [Google Cloud](/release-notes) page, browse and filter all release notes in the [Google Cloud console](https://console.cloud.google.com/release-notes) , or programmatically access release notes in [BigQuery](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=google_cloud_release_notes&t=release_notes&page=table) .

To get the latest product updates delivered to you, add the URL of this page to your [feed reader](https://wikipedia.org/wiki/Comparison_of_feed_aggregators) , or add the [feed URL](https://docs.cloud.google.com/feeds/datastore-release-notes.xml) directly.

## February 02, 2026

Feature

The Firestore databases page in the Google Cloud console now includes a status column. Possible statuses include:

  - Ready
  - Cloning is in progress
  - Restoring from backup is in progress
  - Deleted
  - Failed

For the cloning and restore statuses, the status column updates upon completion.

## December 22, 2025

Libraries

### Python

#### [2.22.0](https://github.com/googleapis/python-datastore/compare/v2.21.0...v2.22.0) (2025-12-12)

##### Bug Fixes

  - remove setup.cfg configuration for creating universal wheels (\#601) ( [df729015](https://github.com/googleapis/python-datastore/commit/df729015) )

### Python

#### [2.23.0](https://github.com/googleapis/python-datastore/compare/v2.22.0...v2.23.0) (2025-12-16)

##### Features

  - support mTLS certificates when available (\#658) ( [85c02328](https://github.com/googleapis/python-datastore/commit/85c02328) )

### Java

#### [2.34.0-rc1](https://github.com/googleapis/java-datastore/compare/v2.33.1...v2.34.0-rc1) (2025-12-16)

##### Features

  - Add FindNearest API to the stable branch ( [3512ba2](https://github.com/googleapis/java-datastore/commit/3512ba2f1bcd358e3c39c36944e05873b3f25f51) )
  - Add firestoreInDatastoreMode for datastore emulator ( [\#1698](https://github.com/googleapis/java-datastore/issues/1698) ) ( [50f106d](https://github.com/googleapis/java-datastore/commit/50f106d4c50884ce471a66c00df322270fe4a91c) )
  - add getNumber to AggregationResult (https://github.com/googleapis/java-datastore/issues/1851) ( [\#1861](https://github.com/googleapis/java-datastore/issues/1861) ) ( [b9c2c3f](https://github.com/googleapis/java-datastore/commit/b9c2c3ff775f7123d701ccacff9bd2ea3718243b) )
  - Add sample code for connection pooling ( [\#1947](https://github.com/googleapis/java-datastore/issues/1947) ) ( [57981db](https://github.com/googleapis/java-datastore/commit/57981db8fb73f35bf72a9c1c5d53bd06dedf0ebc) )
  - add sample code for multiple inequalities indexing consideration query ( [\#1579](https://github.com/googleapis/java-datastore/issues/1579) ) ( [1286792](https://github.com/googleapis/java-datastore/commit/1286792d7b49229d698df652cd117d229a5cd97e) )
  - enable flag for report generation ( [\#1991](https://github.com/googleapis/java-datastore/issues/1991) ) ( [767a558](https://github.com/googleapis/java-datastore/commit/767a558d7cd8b4ba791fe5d304757e660f7935ff) )
  - enable grpc configurator for client-side tracing ( [\#1886](https://github.com/googleapis/java-datastore/issues/1886) ) ( [97004c8](https://github.com/googleapis/java-datastore/commit/97004c85d73541ccfc26e0f4212e3a447d3e4ba6) )
  - enable hermetic library generation ( [\#1462](https://github.com/googleapis/java-datastore/issues/1462) ) ( [d142d9c](https://github.com/googleapis/java-datastore/commit/d142d9c95d91c8cadaf696efc12d6136814938ff) )
  - implement query profile ( [\#1365](https://github.com/googleapis/java-datastore/issues/1365) ) ( [2515ed6](https://github.com/googleapis/java-datastore/commit/2515ed6cf733df84069309a3055a21cdd65c9c90) )
  - introduce `  java.time  ` methods and variables ( [\#1671](https://github.com/googleapis/java-datastore/issues/1671) ) ( [5a78a80](https://github.com/googleapis/java-datastore/commit/5a78a8075867f4b2fc598f0423bd2ab65b559856) )
  - Introducing Tracing with OpenTelemetry API [\#1537](https://github.com/googleapis/java-datastore/issues/1537) ( [\#1576](https://github.com/googleapis/java-datastore/issues/1576) ) ( [5440c22](https://github.com/googleapis/java-datastore/commit/5440c22364074c108450c3a748a6a17d5f1dddda) )
  - Java datastore gapic upgrade ( [\#1824](https://github.com/googleapis/java-datastore/issues/1824) ) ( [a296d43](https://github.com/googleapis/java-datastore/commit/a296d43724c57aba6a69ebed249261e3d367d625) )
  - New PropertyMask field which allows partial commits, lookups, and query results ( [\#1455](https://github.com/googleapis/java-datastore/issues/1455) ) ( [ff5e397](https://github.com/googleapis/java-datastore/commit/ff5e39775446216b4806f55f14dacb7fc8e8854b) )
  - next release from main branch is 2.27.0 ( [\#1781](https://github.com/googleapis/java-datastore/issues/1781) ) ( [d29f47c](https://github.com/googleapis/java-datastore/commit/d29f47cbef9998acdc8b7b0f42d93574dab3cc7f) )
  - next release from main branch is 2.31.0 ( [\#1912](https://github.com/googleapis/java-datastore/issues/1912) ) ( [a74c46b](https://github.com/googleapis/java-datastore/commit/a74c46bfbac8eaf5c97fe653b740e26e7c79f4da) )
  - remove `  @BetaApi  ` annotations from get/setDatabaseId methods ( [\#1272](https://github.com/googleapis/java-datastore/issues/1272) ) ( [2bd9a51](https://github.com/googleapis/java-datastore/commit/2bd9a51122248ee242bbcd4914e219d9d5e435bb) )
  - Support for field update operators in the Datastore API and resolution strategies when there is a conflict at write time ( [b299266](https://github.com/googleapis/java-datastore/commit/b299266e42037b731ee7bbba21dbded73a37323c) )
  - update with latest from main ( [\#2018](https://github.com/googleapis/java-datastore/issues/2018) ) ( [3a0daed](https://github.com/googleapis/java-datastore/commit/3a0daedca7a2ac9c97bc82592e0ba0d2421243c0) )
  - Upgrade protobuf gen code to 4.33 ( [\#2019](https://github.com/googleapis/java-datastore/issues/2019) ) ( [c783809](https://github.com/googleapis/java-datastore/commit/c783809a7b9e27e4d8982e8f2197351e5173203a) )

##### Bug Fixes

  - checksum format ( [\#1178](https://github.com/googleapis/java-datastore/issues/1178) ) ( [410b939](https://github.com/googleapis/java-datastore/commit/410b9397bb9ba480dff6217c0c4c27364e58db49) )
  - deprecate `  databaseId  ` on datastore-v1-proto-client DatastoreOptions ( [\#1190](https://github.com/googleapis/java-datastore/issues/1190) ) ( [12a3d27](https://github.com/googleapis/java-datastore/commit/12a3d27ebc7ca87338ee896fd6ba3e804edd95ce) )
  - **deps:** Update the Java code generator (gapic-generator-java) to 2.31.0 ( [\#1278](https://github.com/googleapis/java-datastore/issues/1278) ) ( [01cced6](https://github.com/googleapis/java-datastore/commit/01cced66613bc10ba71cc80166119e321915ec34) )
  - **deps:** Update the Java code generator (gapic-generator-java) to 2.32.0 ( [\#1293](https://github.com/googleapis/java-datastore/issues/1293) ) ( [f4ee0cb](https://github.com/googleapis/java-datastore/commit/f4ee0cb4668077f9fb6b0ede1ea69b9033748fe9) )
  - **deps:** Update the Java code generator (gapic-generator-java) to 2.37.0 ( [\#1355](https://github.com/googleapis/java-datastore/issues/1355) ) ( [bcc5668](https://github.com/googleapis/java-datastore/commit/bcc5668039d4dd2055e9666a65fcda3984fc33b5) )
  - **deps:** Update the Java code generator (gapic-generator-java) to 2.39.0 ( [\#1406](https://github.com/googleapis/java-datastore/issues/1406) ) ( [b265fb3](https://github.com/googleapis/java-datastore/commit/b265fb3c3b8ebc972edbe5a7beae816379846dac) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.46.1 ( [678eee2](https://github.com/googleapis/java-datastore/commit/678eee2dfb6d447a852edd436137f8ebfbe50d74) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.47.0 ( [b299266](https://github.com/googleapis/java-datastore/commit/b299266e42037b731ee7bbba21dbded73a37323c) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.51.0 ( [106ee4d](https://github.com/googleapis/java-datastore/commit/106ee4dd7ca4dd9e59a5419f59b8625680e60f15) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.51.1 ( [90d8b30](https://github.com/googleapis/java-datastore/commit/90d8b3034d5a583d880a822d1e763035a2120f4a) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.52.0 ( [9594024](https://github.com/googleapis/java-datastore/commit/95940241de9f324000d52dc80b3106aedefd481e) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.53.0 ( [be0d0cd](https://github.com/googleapis/java-datastore/commit/be0d0cd960b9254d26404d9331b78dee1104cf0a) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.53.0 ( [93e45ed](https://github.com/googleapis/java-datastore/commit/93e45edf335f06fd707ce64398c8b02d2a433f6f) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.54.0 ( [b9b302b](https://github.com/googleapis/java-datastore/commit/b9b302bb6c8bb1c8d8b175b776b2f65317511987) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.55.1 ( [ba1ad98](https://github.com/googleapis/java-datastore/commit/ba1ad98cce4c0feae13a370ea0581d15674dd43c) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.56.2 ( [1210f32](https://github.com/googleapis/java-datastore/commit/1210f32662e7aafd2e170643bedbb851f40f3646) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.59.0 ( [910a6c2](https://github.com/googleapis/java-datastore/commit/910a6c20cb23f441ede5cd75972c65adbb8752e8) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.60.2 ( [06372cd](https://github.com/googleapis/java-datastore/commit/06372cd63a7ce35747d90c62cc1d57be0a6ffb37) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.61.0 ( [c7bd68d](https://github.com/googleapis/java-datastore/commit/c7bd68de82ec06f06c41cd12e87cc96a337dcd02) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.62.0 ( [90f5526](https://github.com/googleapis/java-datastore/commit/90f552624627b3ca6fde4b4241b66893019174dd) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.63.0 ( [b9b95cb](https://github.com/googleapis/java-datastore/commit/b9b95cb0b08ec393f714f885e511443c1e044a0e) )
  - **deps:** update the Java code generator (gapic-generator-java) to 2.64.1 ( [216e771](https://github.com/googleapis/java-datastore/commit/216e771f9181f03f4add7e35bf11c5f64f80b6a7) )
  - **doc:** Add discriptions for TransactionCallable interface ( [\#1644](https://github.com/googleapis/java-datastore/issues/1644) ) ( [173a883](https://github.com/googleapis/java-datastore/commit/173a88330cc5693f54504348cf39bf3191db2250) )
  - **doc:** Fix return types for batch interface ( [\#1645](https://github.com/googleapis/java-datastore/issues/1645) ) ( [1189211](https://github.com/googleapis/java-datastore/commit/11892116f0fb8eacb711a8f48e780e48a232f987) )
  - Fix emulator command arg data-dir ( [\#1695](https://github.com/googleapis/java-datastore/issues/1695) ) ( [9d53195](https://github.com/googleapis/java-datastore/commit/9d531957da3f017f0702a126601eaa8afe3113d6) )
  - Migrate off TextPrinter's deprecated methods ( [\#1452](https://github.com/googleapis/java-datastore/issues/1452) ) ( [c3c1317](https://github.com/googleapis/java-datastore/commit/c3c131735863d71971110e2ac7ac0244ce16ee92) )
  - next release candidate ( [4824f2b](https://github.com/googleapis/java-datastore/commit/4824f2b214d3addcf25235f43cc9bf4a2ebb0a76) )
  - remove 500 char path name limit ( [\#1865](https://github.com/googleapis/java-datastore/issues/1865) ) ( [1097175](https://github.com/googleapis/java-datastore/commit/10971752310d8b1794c8e77041b582707142b328) )
  - remove deprecated `  databaseId  ` field in DatastoreOptions ( [\#1237](https://github.com/googleapis/java-datastore/issues/1237) ) ( [05e25e5](https://github.com/googleapis/java-datastore/commit/05e25e5d31f72f9cdedbb5efa85c64b55ccbc405) )
  - remove QueryMode field from RunAggregationQueryRequest ( [c1e7c62](https://github.com/googleapis/java-datastore/commit/c1e7c6201e0e35469df1492a4ce61bf6a095f8be) )
  - remove QueryMode field from RunQueryRequest ( [c1e7c62](https://github.com/googleapis/java-datastore/commit/c1e7c6201e0e35469df1492a4ce61bf6a095f8be) )
  - remove ResultSetStats field from RunAggregationQueryResponse ( [c1e7c62](https://github.com/googleapis/java-datastore/commit/c1e7c6201e0e35469df1492a4ce61bf6a095f8be) )
  - remove ResultSetStats field from RunQueryResponse ( [c1e7c62](https://github.com/googleapis/java-datastore/commit/c1e7c6201e0e35469df1492a4ce61bf6a095f8be) )
  - remove types QueryMode, QueryPlan, ResultSetStats ( [\#1304](https://github.com/googleapis/java-datastore/issues/1304) ) ( [c1e7c62](https://github.com/googleapis/java-datastore/commit/c1e7c6201e0e35469df1492a4ce61bf6a095f8be) )
  - **sample:** change update entity sample to use transaction ( [\#1633](https://github.com/googleapis/java-datastore/issues/1633) ) ( [c44f17a](https://github.com/googleapis/java-datastore/commit/c44f17a7bb93d688367611ee2533c59c940ae61f) )
  - set the correct database id on the key parent when calling Key\#getParent ( [\#1457](https://github.com/googleapis/java-datastore/issues/1457) ) ( [992815d](https://github.com/googleapis/java-datastore/commit/992815d9989d04f7b371dfa320ed17894626a07f) )
  - Update opentelemetry-sdk dependency to be test-only ( [\#1595](https://github.com/googleapis/java-datastore/issues/1595) ) ( [9d719e8](https://github.com/googleapis/java-datastore/commit/9d719e809ea830d8602399b72e432580f14ae6bd) )
  - Update opentelemetry.version to 1.42.1 to match the BOM version ( [\#1598](https://github.com/googleapis/java-datastore/issues/1598) ) ( [23c5c26](https://github.com/googleapis/java-datastore/commit/23c5c2662117370c66c611604c56b878d41f4738) )

##### Dependencies

  - **autogen:** set packed = false on field\_behavior extension ( [\#1320](https://github.com/googleapis/java-datastore/issues/1320) ) ( [9cfa1c3](https://github.com/googleapis/java-datastore/commit/9cfa1c37a8a86fcb09ec896dc9219e4416ff2fef) )
  - Manage Opentelemetry version from Shared-Deps ( [\#1995](https://github.com/googleapis/java-datastore/issues/1995) ) ( [5f6c500](https://github.com/googleapis/java-datastore/commit/5f6c500d3fb092d87669550ff882782b10199a03) )
  - update actions/checkout action to v4 ( [\#1390](https://github.com/googleapis/java-datastore/issues/1390) ) ( [80dbca1](https://github.com/googleapis/java-datastore/commit/80dbca1246facf21b08d33e5c6a09b9708b6ce63) )
  - update dependency com.google.cloud:gapic-libraries-bom to v1.43.0 ( [\#1584](https://github.com/googleapis/java-datastore/issues/1584) ) ( [fae3b74](https://github.com/googleapis/java-datastore/commit/fae3b74eaa3494a27fd43f56435c01e8fc09e5ee) )
  - update dependency com.google.cloud:gapic-libraries-bom to v1.48.0 ( [\#1605](https://github.com/googleapis/java-datastore/issues/1605) ) ( [5c6a678](https://github.com/googleapis/java-datastore/commit/5c6a67844f7b5d4c7001cccd1bed3d0d56be6e90) )
  - update dependency com.google.cloud:gapic-libraries-bom to v1.49.0 ( [\#1693](https://github.com/googleapis/java-datastore/issues/1693) ) ( [8160c28](https://github.com/googleapis/java-datastore/commit/8160c2895e947c118cea24e92d9a31a1fdf4653f) )
  - update dependency com.google.cloud:gapic-libraries-bom to v1.50.0 ( [\#1708](https://github.com/googleapis/java-datastore/issues/1708) ) ( [b78660f](https://github.com/googleapis/java-datastore/commit/b78660f3866ce5c1198db4590b5e1f645170ecff) )
  - update dependency com.google.cloud:gapic-libraries-bom to v1.51.0 ( [\#1726](https://github.com/googleapis/java-datastore/issues/1726) ) ( [89f31a8](https://github.com/googleapis/java-datastore/commit/89f31a88d346193c9a5533de3e38c9088db30043) )
  - update dependency com.google.cloud:gapic-libraries-bom to v1.52.0 ( [\#1747](https://github.com/googleapis/java-datastore/issues/1747) ) ( [592072b](https://github.com/googleapis/java-datastore/commit/592072b194706e63a7fd4a6f6230377e8f4b729d) )
  - update dependency com.google.cloud:gapic-libraries-bom to v1.53.0 ( [\#1779](https://github.com/googleapis/java-datastore/issues/1779) ) ( [8369118](https://github.com/googleapis/java-datastore/commit/8369118994e9a18b888a7779376fea7e22b219ed) )
  - update dependency com.google.cloud:gapic-libraries-bom to v1.60.0 ( [\#1799](https://github.com/googleapis/java-datastore/issues/1799) ) ( [bf2a33c](https://github.com/googleapis/java-datastore/commit/bf2a33c32a04b978a19fd6dfbe845769c921fa4f) )
  - update dependency com.google.cloud:gapic-libraries-bom to v1.61.0 ( [\#1901](https://github.com/googleapis/java-datastore/issues/1901) ) ( [beeb125](https://github.com/googleapis/java-datastore/commit/beeb125efc842776facfa67742bdf8b6c167e9f2) )
  - update dependency com.google.cloud:google-cloud-shared-dependencies to v3.16.0 ( [\#1195](https://github.com/googleapis/java-datastore/issues/1195) ) ( [6f0cad7](https://github.com/googleapis/java-datastore/commit/6f0cad7268cee6347d34125c14c1133b80c840d7) )
  - update dependency com.google.cloud:google-cloud-shared-dependencies to v3.16.1 ( [\#1198](https://github.com/googleapis/java-datastore/issues/1198) ) ( [8062be9](https://github.com/googleapis/java-datastore/commit/8062be94b00fe2967e592f3d0a35751f0d11a013) )
  - update dependency com.google.cloud:google-cloud-shared-dependencies to v3.17.0 ( [\#1206](https://github.com/googleapis/java-datastore/issues/1206) ) ( [2ad068b](https://github.com/googleapis/java-datastore/commit/2ad068b115c6ff7c59394fdba5e0e445028a3fee) )
  - update dependency com.google.cloud:google-cloud-shared-dependencies to v3.18.0 ( [\#1215](https://github.com/googleapis/java-datastore/issues/1215) ) ( [aa82f01](https://github.com/googleapis/java-datastore/commit/aa82f019bcf90f99e6d3d2c96a52d8f2b9a8d27a) )
  - update dependency com.google.cloud:google-cloud-shared-dependencies to v3.19.0 ( [\#1226](https://github.com/googleapis/java-datastore/issues/1226) ) ( [970ac96](https://github.com/googleapis/java-datastore/commit/970ac9652ad16848ccfb26ce248e66956693be9e) )
  - update dependency com.google.cloud:google-cloud-shared-dependencies to v3.20.0 ( [\#1247](https://github.com/googleapis/java-datastore/issues/1247) ) ( [c4e3533](https://github.com/googleapis/java-datastore/commit/c4e3533fe357827cc25d0f029e5a83ced31db12a) )
  - update dependency com.google.cloud:google-cloud-shared-dependencies to v3.21.0 ( [\#1280](https://github.com/googleapis/java-datastore/issues/1280) ) ( [ac253dc](https://github.com/googleapis/java-datastore/commit/ac253dca1add844124ca03039a996196e09a1759) )
  - update dependency com.google.cloud:google-cloud-shared-dependencies to v3.22.0 ( [\#1291](https://github.com/googleapis/java-datastore/issues/1291) ) ( [5a5c78e](https://github.com/googleapis/java-datastore/commit/5a5c78e01a765d3ebce547b54d7d6d16c0894fb2) )
  - update dependency com.google.cloud:google-cloud-shared-dependencies to v3.23.0 ( [\#1301](https://github.com/googleapis/java-datastore/issues/1301) ) ( [ac947a5](https://github.com/googleapis/java-datastore/commit/ac947a545235fa41f0ffb52c4e3a0ffc498991e1) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.24.0 ( [\#1310](https://github.com/googleapis/java-datastore/issues/1310) ) ( [26e5f98](https://github.com/googleapis/java-datastore/commit/26e5f9873c4df1815406020a6c22e4a20638f959) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.25.0 ( [\#1333](https://github.com/googleapis/java-datastore/issues/1333) ) ( [0e64a7d](https://github.com/googleapis/java-datastore/commit/0e64a7da73a3b6d40d5952bf09372d631a7d247b) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.27.0 ( [\#1352](https://github.com/googleapis/java-datastore/issues/1352) ) ( [124d7ca](https://github.com/googleapis/java-datastore/commit/124d7cab46e2fa1ba654369887fb10ffb3f8eaef) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.28.0 ( [\#1372](https://github.com/googleapis/java-datastore/issues/1372) ) ( [09db2a7](https://github.com/googleapis/java-datastore/commit/09db2a75fa714a909bc6fa9b43a9213ae6467c84) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.28.1 ( [\#1373](https://github.com/googleapis/java-datastore/issues/1373) ) ( [c6e63e5](https://github.com/googleapis/java-datastore/commit/c6e63e5f876fdda953935d09f0536a90a98a812c) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.29.0 ( [\#1403](https://github.com/googleapis/java-datastore/issues/1403) ) ( [d23dc4c](https://github.com/googleapis/java-datastore/commit/d23dc4c26a95f2c323ade4db9a88d5435a173be8) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.30.0 ( [\#1426](https://github.com/googleapis/java-datastore/issues/1426) ) ( [ac3a1c1](https://github.com/googleapis/java-datastore/commit/ac3a1c10f64c8338346f8fb39f4857f47e8fc639) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.30.1 ( [\#1443](https://github.com/googleapis/java-datastore/issues/1443) ) ( [79f6c46](https://github.com/googleapis/java-datastore/commit/79f6c46bdbabc66082f23e9562ee9541e0fdeac9) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.31.0 ( [\#1471](https://github.com/googleapis/java-datastore/issues/1471) ) ( [42c643d](https://github.com/googleapis/java-datastore/commit/42c643d78562c5cbd6c17c29a0a124be8d05198a) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.32.0 ( [\#1492](https://github.com/googleapis/java-datastore/issues/1492) ) ( [d940c93](https://github.com/googleapis/java-datastore/commit/d940c937959942d753f9215e7ce940ab6742be46) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.33.0 ( [\#1531](https://github.com/googleapis/java-datastore/issues/1531) ) ( [9e52395](https://github.com/googleapis/java-datastore/commit/9e52395f7ee71315331790284d35e7aad2f387ed) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.34.0 ( [\#1547](https://github.com/googleapis/java-datastore/issues/1547) ) ( [8c5f595](https://github.com/googleapis/java-datastore/commit/8c5f5954d88732ab929b4477a3f15b0052adc2ff) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.35.0 ( [\#1561](https://github.com/googleapis/java-datastore/issues/1561) ) ( [5a79fd8](https://github.com/googleapis/java-datastore/commit/5a79fd8d1202e65c02423fe40402c41af6050efa) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.36.0 ( [\#1590](https://github.com/googleapis/java-datastore/issues/1590) ) ( [2db9e43](https://github.com/googleapis/java-datastore/commit/2db9e439189baf8f97127f6cff1de5d47efb0073) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.36.1 ( [\#1602](https://github.com/googleapis/java-datastore/issues/1602) ) ( [e1b7d4b](https://github.com/googleapis/java-datastore/commit/e1b7d4b205312d7d4c2a285f3d1f61388da65c83) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.38.0 ( [\#1632](https://github.com/googleapis/java-datastore/issues/1632) ) ( [6453f1e](https://github.com/googleapis/java-datastore/commit/6453f1e44f370a13434ef68295ae5638612032c8) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.39.0 ( [\#1640](https://github.com/googleapis/java-datastore/issues/1640) ) ( [fe61f66](https://github.com/googleapis/java-datastore/commit/fe61f6691a5e3c8fbfc974b6fe613a69652241ca) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.41.1 ( [\#1703](https://github.com/googleapis/java-datastore/issues/1703) ) ( [bf9537f](https://github.com/googleapis/java-datastore/commit/bf9537f81b6e7cc2252ad0183fb87db656b009d7) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.42.0 ( [\#1725](https://github.com/googleapis/java-datastore/issues/1725) ) ( [1cbaf22](https://github.com/googleapis/java-datastore/commit/1cbaf22cf557aec606dce7a5ca5d3ebe620a9339) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.43.0 ( [\#1737](https://github.com/googleapis/java-datastore/issues/1737) ) ( [7272a41](https://github.com/googleapis/java-datastore/commit/7272a4197a0d7fb97ee039ccb88ac13a1ec037d1) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.44.0 ( [\#1769](https://github.com/googleapis/java-datastore/issues/1769) ) ( [7a86509](https://github.com/googleapis/java-datastore/commit/7a8650939e652fc3b384053454d6ef5084bb1508) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.45.1 ( [\#1791](https://github.com/googleapis/java-datastore/issues/1791) ) ( [ab5ac8e](https://github.com/googleapis/java-datastore/commit/ab5ac8e6407541520fabb4504fcce0d675347f63) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.46.2 ( [\#1823](https://github.com/googleapis/java-datastore/issues/1823) ) ( [4d2026c](https://github.com/googleapis/java-datastore/commit/4d2026c330009becc201a95c42af365cc83b8ea5) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.47.0 ( [\#1841](https://github.com/googleapis/java-datastore/issues/1841) ) ( [ac393e6](https://github.com/googleapis/java-datastore/commit/ac393e61e517d30b534be3e99070c210081c4f0b) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.48.0 ( [\#1847](https://github.com/googleapis/java-datastore/issues/1847) ) ( [7ed3232](https://github.com/googleapis/java-datastore/commit/7ed32321a5c84c4b2f61094e4c4adb5e36e5bc1b) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.49.0 ( [\#1860](https://github.com/googleapis/java-datastore/issues/1860) ) ( [0eff028](https://github.com/googleapis/java-datastore/commit/0eff0284bf78152341e1692ffc57930f62ec01dc) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.50.0 ( [\#1897](https://github.com/googleapis/java-datastore/issues/1897) ) ( [a8d99cd](https://github.com/googleapis/java-datastore/commit/a8d99cde26c38376b596f44379f4d069b25339b2) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.50.1 ( [\#1908](https://github.com/googleapis/java-datastore/issues/1908) ) ( [b10e0f0](https://github.com/googleapis/java-datastore/commit/b10e0f0748decf06574fc0eb7ddba33ee5ece1a7) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.50.2 ( [\#1926](https://github.com/googleapis/java-datastore/issues/1926) ) ( [1ecdf37](https://github.com/googleapis/java-datastore/commit/1ecdf377b2a6ccb2ffd231744726807b0493df79) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.51.0 ( [\#1936](https://github.com/googleapis/java-datastore/issues/1936) ) ( [a25433f](https://github.com/googleapis/java-datastore/commit/a25433f805f957dc0beebaeef466aa20f14f8ccc) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.52.0 ( [\#1944](https://github.com/googleapis/java-datastore/issues/1944) ) ( [30a6e28](https://github.com/googleapis/java-datastore/commit/30a6e2856ee87568f14bbe94fe5918a4ecea4612) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.52.1 ( [\#1963](https://github.com/googleapis/java-datastore/issues/1963) ) ( [833a34a](https://github.com/googleapis/java-datastore/commit/833a34a7e5ab1194d2ac8ebf097d7c300d7e8d37) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.52.2 ( [\#1969](https://github.com/googleapis/java-datastore/issues/1969) ) ( [2243471](https://github.com/googleapis/java-datastore/commit/22434714d50d9da1c6034bf9dbec745a62abc731) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.52.3 ( [\#1973](https://github.com/googleapis/java-datastore/issues/1973) ) ( [141ec94](https://github.com/googleapis/java-datastore/commit/141ec943cd6e619a64a48e14053119aeb5238817) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.53.0 ( [\#1980](https://github.com/googleapis/java-datastore/issues/1980) ) ( [1520b7c](https://github.com/googleapis/java-datastore/commit/1520b7c4ac51139c1c8809a4ead990d558f6c705) )
  - update dependency com.google.cloud:sdk-platform-java-config to v3.54.1 ( [\#1994](https://github.com/googleapis/java-datastore/issues/1994) ) ( [11265fd](https://github.com/googleapis/java-datastore/commit/11265fdee02b429803d2d2c7d1e7f5a735e11757) )
  - update dependency com.google.errorprone:error\_prone\_core to v2.22.0 ( [\#1194](https://github.com/googleapis/java-datastore/issues/1194) ) ( [b8f108a](https://github.com/googleapis/java-datastore/commit/b8f108a3d013b5b54c519db24b40dd63e4855240) )
  - update dependency com.google.errorprone:error\_prone\_core to v2.23.0 ( [\#1213](https://github.com/googleapis/java-datastore/issues/1213) ) ( [c57db43](https://github.com/googleapis/java-datastore/commit/c57db43c783ba6ec16a55d470664990e932971ef) )
  - update dependency com.google.errorprone:error\_prone\_core to v2.24.1 ( [\#1274](https://github.com/googleapis/java-datastore/issues/1274) ) ( [86cd785](https://github.com/googleapis/java-datastore/commit/86cd7856463c5039601afc10fecc1b28727d4906) )
  - update dependency com.google.errorprone:error\_prone\_core to v2.25.0 ( [\#1339](https://github.com/googleapis/java-datastore/issues/1339) ) ( [0c6702e](https://github.com/googleapis/java-datastore/commit/0c6702e27917b976c76a0d44d3f5d550418310be) )
  - update dependency com.google.errorprone:error\_prone\_core to v2.26.0 ( [\#1361](https://github.com/googleapis/java-datastore/issues/1361) ) ( [9442766](https://github.com/googleapis/java-datastore/commit/9442766ad61b0c1001d36ecfc0668308838b4a83) )
  - update dependency com.google.errorprone:error\_prone\_core to v2.26.1 ( [\#1363](https://github.com/googleapis/java-datastore/issues/1363) ) ( [05fe5bc](https://github.com/googleapis/java-datastore/commit/05fe5bccf97dae92c00f2eead98424771cb321fd) )
  - update dependency com.google.errorprone:error\_prone\_core to v2.27.0 ( [\#1411](https://github.com/googleapis/java-datastore/issues/1411) ) ( [a3f5a2c](https://github.com/googleapis/java-datastore/commit/a3f5a2c24bff408479541e08278e888cf3166727) )
  - update dependency com.google.errorprone:error\_prone\_core to v2.27.1 ( [\#1421](https://github.com/googleapis/java-datastore/issues/1421) ) ( [48d7daf](https://github.com/googleapis/java-datastore/commit/48d7dafc0c7a49e95bf41d29865ac872b0de0faf) )
  - update dependency com.google.errorprone:error\_prone\_core to v2.28.0 ( [\#1469](https://github.com/googleapis/java-datastore/issues/1469) ) ( [e3fac2b](https://github.com/googleapis/java-datastore/commit/e3fac2bf9992fcb2e91319df0520094865de2d49) )
  - update dependency com.google.errorprone:error\_prone\_core to v2.31.0 ( [\#1523](https://github.com/googleapis/java-datastore/issues/1523) ) ( [8d3af32](https://github.com/googleapis/java-datastore/commit/8d3af322fb56032cd7a9d29e60fd93d1f3e7e632) )
  - update dependency com.google.guava:guava-testlib to v33.1.0-jre ( [\#1368](https://github.com/googleapis/java-datastore/issues/1368) ) ( [0195345](https://github.com/googleapis/java-datastore/commit/0195345630f404bbcaf1601ded8a8e2011fc3e6e) )
  - update dependency com.google.guava:guava-testlib to v33.2.0-jre ( [\#1422](https://github.com/googleapis/java-datastore/issues/1422) ) ( [5a5dfdf](https://github.com/googleapis/java-datastore/commit/5a5dfdfb0855cf485b875ab071b79979d24f98dd) )
  - update dependency com.google.guava:guava-testlib to v33.2.1-jre ( [\#1470](https://github.com/googleapis/java-datastore/issues/1470) ) ( [614e930](https://github.com/googleapis/java-datastore/commit/614e930f2bdccc517d4733e5fb7f3cefad696a20) )
  - update dependency com.google.guava:guava-testlib to v33.3.0-jre ( [\#1548](https://github.com/googleapis/java-datastore/issues/1548) ) ( [18ba37f](https://github.com/googleapis/java-datastore/commit/18ba37f60b5b3e69c95f6e55a28daf8c0de82ba9) )
  - update dependency com.google.guava:guava-testlib to v33.3.1-jre ( [\#1592](https://github.com/googleapis/java-datastore/issues/1592) ) ( [5d078a4](https://github.com/googleapis/java-datastore/commit/5d078a4b294d071716f51f0d4b9baa5d65a0fe90) )
  - update dependency com.google.guava:guava-testlib to v33.4.0-jre ( [\#1694](https://github.com/googleapis/java-datastore/issues/1694) ) ( [b91a2af](https://github.com/googleapis/java-datastore/commit/b91a2af534eb7568ec86a0b27a80a6bd2943af7b) )
  - update dependency com.google.testparameterinjector:test-parameter-injector to v1.17 ( [\#1585](https://github.com/googleapis/java-datastore/issues/1585) ) ( [8f74a49](https://github.com/googleapis/java-datastore/commit/8f74a49c5982d00bd168e78671163683f7b41126) )
  - update dependency org.easymock:easymock to v5.4.0 ( [\#1482](https://github.com/googleapis/java-datastore/issues/1482) ) ( [ee788a1](https://github.com/googleapis/java-datastore/commit/ee788a162841994e09a61bb81b94cbe93353a78e) )
  - update dependency org.easymock:easymock to v5.5.0 ( [\#1666](https://github.com/googleapis/java-datastore/issues/1666) ) ( [0333b07](https://github.com/googleapis/java-datastore/commit/0333b0744bab87afe78dad1c17f6811d3dec47e6) )
  - update dependency org.easymock:easymock to v5.6.0 ( [\#1858](https://github.com/googleapis/java-datastore/issues/1858) ) ( [acc1513](https://github.com/googleapis/java-datastore/commit/acc1513ad90e8da6743e618322bae075bac4ac46) )
  - update dependency org.graalvm.buildtools:junit-platform-native to v0.9.26 ( [\#1176](https://github.com/googleapis/java-datastore/issues/1176) ) ( [76e3a71](https://github.com/googleapis/java-datastore/commit/76e3a71560222894513a485cb91cec7161276e3c) )
  - update dependency org.graalvm.buildtools:junit-platform-native to v0.9.27 ( [\#1192](https://github.com/googleapis/java-datastore/issues/1192) ) ( [aa3bca1](https://github.com/googleapis/java-datastore/commit/aa3bca10de19350cabc244426ebc284c64cb7344) )
  - update dependency org.graalvm.buildtools:junit-platform-native to v0.9.28 ( [\#1216](https://github.com/googleapis/java-datastore/issues/1216) ) ( [ce4eff2](https://github.com/googleapis/java-datastore/commit/ce4eff24aae8d1e6e02558e627c033dc138891e6) )
  - update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.26 ( [\#1177](https://github.com/googleapis/java-datastore/issues/1177) ) ( [7733004](https://github.com/googleapis/java-datastore/commit/7733004aff34bb8b4b8addccc68e75080f0f33a5) )
  - update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.27 ( [\#1193](https://github.com/googleapis/java-datastore/issues/1193) ) ( [a628255](https://github.com/googleapis/java-datastore/commit/a628255dffc2e8f871df699ebe7a94e4b75eb4b9) )
  - update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.28 ( [\#1217](https://github.com/googleapis/java-datastore/issues/1217) ) ( [7d56b3c](https://github.com/googleapis/java-datastore/commit/7d56b3cee53e0852873896f7fd22a0414d4b7d83) )
  - update dependency org.junit.vintage:junit-vintage-engine to v5.10.1 ( [\#1230](https://github.com/googleapis/java-datastore/issues/1230) ) ( [05c7fc6](https://github.com/googleapis/java-datastore/commit/05c7fc69d52f5a9026a6529f638fe6164860e8f9) )
  - Update gapic-generator-java to 2.26.0 ( [\#1197](https://github.com/googleapis/java-datastore/issues/1197) ) ( [2540282](https://github.com/googleapis/java-datastore/commit/2540282653d8f8f06a71568c81eca8d3cb70f00f) )
  - update googleapis/sdk-platform-java action to v2.48.0 ( [\#1628](https://github.com/googleapis/java-datastore/issues/1628) ) ( [d3bce79](https://github.com/googleapis/java-datastore/commit/d3bce79467254b3128a8f16d5754e91d29ece525) )
  - update googleapis/sdk-platform-java action to v2.49.0 ( [\#1638](https://github.com/googleapis/java-datastore/issues/1638) ) ( [57598d7](https://github.com/googleapis/java-datastore/commit/57598d7d59cd6917f23a653403613e4edc160c64) )
  - update googleapis/sdk-platform-java action to v2.53.0 ( [\#1738](https://github.com/googleapis/java-datastore/issues/1738) ) ( [b8a7a5d](https://github.com/googleapis/java-datastore/commit/b8a7a5d5d8700ccccb643162843e3043396a9444) )
  - update googleapis/sdk-platform-java action to v2.57.0 ( [\#1842](https://github.com/googleapis/java-datastore/issues/1842) ) ( [0745906](https://github.com/googleapis/java-datastore/commit/0745906bbdd8819ac2ccaafa301c8f4b4fd20be4) )
  - update googleapis/sdk-platform-java action to v2.58.0 ( [\#1853](https://github.com/googleapis/java-datastore/issues/1853) ) ( [eef820d](https://github.com/googleapis/java-datastore/commit/eef820d017f5e00245924d551abe172a2a39e29f) )
  - update googleapis/sdk-platform-java action to v2.59.1 ( [\#1880](https://github.com/googleapis/java-datastore/issues/1880) ) ( [4fb9929](https://github.com/googleapis/java-datastore/commit/4fb992943152bb4533e0bbd80e373de61f5ec864) )
  - update googleapis/sdk-platform-java action to v2.60.0 ( [\#1898](https://github.com/googleapis/java-datastore/issues/1898) ) ( [0921f86](https://github.com/googleapis/java-datastore/commit/0921f869ff4a19e7c0fe918aea0896922e9a18af) )
  - Update protobuf to 25.2 in WORKSPACE ( [\#1311](https://github.com/googleapis/java-datastore/issues/1311) ) ( [3f4ae83](https://github.com/googleapis/java-datastore/commit/3f4ae83b20f160eaccd9de17582d54d8222dd015) )
  - update sdk platform java dependencies ( [\#1617](https://github.com/googleapis/java-datastore/issues/1617) ) ( [6eaff23](https://github.com/googleapis/java-datastore/commit/6eaff23f9de25ae6ad2a4fea67c0b65a243c08fd) )
  - update sdk platform java dependencies ( [\#1662](https://github.com/googleapis/java-datastore/issues/1662) ) ( [b4d3ab9](https://github.com/googleapis/java-datastore/commit/b4d3ab9a72bb2a4dff59bf54abcc5d9536b2596b) )
  - update sdk platform java dependencies ( [\#1685](https://github.com/googleapis/java-datastore/issues/1685) ) ( [4372350](https://github.com/googleapis/java-datastore/commit/4372350117ba57903f510512a383339b6a4ea47c) )
  - update sdk-platform-java-config to 3.55.0-rc1 ( [\#2017](https://github.com/googleapis/java-datastore/issues/2017) ) ( [a67694b](https://github.com/googleapis/java-datastore/commit/a67694b3b0c3e8864371c9d9cc1689d69d204ebc) )

##### Documentation

  - Update gapic upgrade installation instructions ( [\#1677](https://github.com/googleapis/java-datastore/issues/1677) ) ( [b3fbfcc](https://github.com/googleapis/java-datastore/commit/b3fbfcc9654bc63bf0d8f3025641d8c50a24ef97) )

## December 15, 2025

Libraries

### Java

#### [2.33.1](https://github.com/googleapis/java-datastore/compare/v2.33.0...v2.33.1) (2025-12-11)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.64.2 ( [b5f1285](https://github.com/googleapis/java-datastore/commit/b5f1285bb783c004464b0f7e8b1fcea567ea22d5) )

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.54.2 ( [\#2011](https://github.com/googleapis/java-datastore/issues/2011) ) ( [c2062e7](https://github.com/googleapis/java-datastore/commit/c2062e77f0ae50981ff381bd82151720f31aa83a) )
  - Update googleapis/sdk-platform-java action to v2.64.2 ( [\#2012](https://github.com/googleapis/java-datastore/issues/2012) ) ( [3ad3168](https://github.com/googleapis/java-datastore/commit/3ad31689197a97d3496ae10fa3338d15d9df022f) )

## November 17, 2025

Libraries

### Java

#### [2.33.0](https://github.com/googleapis/java-datastore/compare/v2.32.3...v2.33.0) (2025-11-13)

##### Features

  - Enable flag for report generation ( [\#1991](https://github.com/googleapis/java-datastore/issues/1991) ) ( [767a558](https://github.com/googleapis/java-datastore/commit/767a558d7cd8b4ba791fe5d304757e660f7935ff) )
  - gRPC is supported for datastore.

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.64.1 ( [216e771](https://github.com/googleapis/java-datastore/commit/216e771f9181f03f4add7e35bf11c5f64f80b6a7) )

##### Dependencies

  - Manage Opentelemetry version from Shared-Deps ( [\#1995](https://github.com/googleapis/java-datastore/issues/1995) ) ( [5f6c500](https://github.com/googleapis/java-datastore/commit/5f6c500d3fb092d87669550ff882782b10199a03) )
  - Update dependency com.google.cloud:sdk-platform-java-config to v3.54.1 ( [\#1994](https://github.com/googleapis/java-datastore/issues/1994) ) ( [11265fd](https://github.com/googleapis/java-datastore/commit/11265fdee02b429803d2d2c7d1e7f5a735e11757) )

## October 27, 2025

Feature

The [database clone feature](https://docs.cloud.google.com/datastore/docs/manage-databases#clone-database) is now supported at the General Availability ( [GA](https://cloud.google.com/products#product-launch-stages) ) level.

Libraries

### Go

#### [1.21.0](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.20.0...datastore/v1.21.0) (2025-10-20)

##### Features

  - **datastore:** Support field transforms ( [\#12400](https://github.com/googleapis/google-cloud-go/issues/12400) ) ( [7defdd0](https://github.com/googleapis/google-cloud-go/commit/7defdd0a9817c8dfcc17d1e739e9e96680fc79ac) )

##### Bug Fixes

  - **datastore:** Resolve data race on transaction state ( [\#12912](https://github.com/googleapis/google-cloud-go/issues/12912) ) ( [011b148](https://github.com/googleapis/google-cloud-go/commit/011b148ca07ff0464f8d9e46742211622a1a45a9) ), refs [\#11038](https://github.com/googleapis/google-cloud-go/issues/11038)
  - **datastore:** Upgrade gRPC service registration func ( [8fffca2](https://github.com/googleapis/google-cloud-go/commit/8fffca2819fa3dc858c213aa0c503e0df331b084) )

### Java

#### [2.32.3](https://github.com/googleapis/java-datastore/compare/v2.32.2...v2.32.3) (2025-10-20)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.63.0 ( [b9b95cb](https://github.com/googleapis/java-datastore/commit/b9b95cb0b08ec393f714f885e511443c1e044a0e) )

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.53.0 ( [\#1980](https://github.com/googleapis/java-datastore/issues/1980) ) ( [1520b7c](https://github.com/googleapis/java-datastore/commit/1520b7c4ac51139c1c8809a4ead990d558f6c705) )

## October 06, 2025

Libraries

### Java

#### [2.32.1](https://github.com/googleapis/java-datastore/compare/v2.32.0...v2.32.1) (2025-09-26)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.52.2 ( [\#1969](https://github.com/googleapis/java-datastore/issues/1969) ) ( [2243471](https://github.com/googleapis/java-datastore/commit/22434714d50d9da1c6034bf9dbec745a62abc731) )

### Java

#### [2.32.2](https://github.com/googleapis/java-datastore/compare/v2.32.1...v2.32.2) (2025-10-04)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.52.3 ( [\#1973](https://github.com/googleapis/java-datastore/issues/1973) ) ( [141ec94](https://github.com/googleapis/java-datastore/commit/141ec943cd6e619a64a48e14053119aeb5238817) )

## September 15, 2025

Libraries

### Java

#### [2.32.0](https://github.com/googleapis/java-datastore/compare/v2.31.4...v2.32.0) (2025-09-12)

##### Features

  - Add sample code for connection pooling ( [\#1947](https://github.com/googleapis/java-datastore/issues/1947) ) ( [57981db](https://github.com/googleapis/java-datastore/commit/57981db8fb73f35bf72a9c1c5d53bd06dedf0ebc) )

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.52.1 ( [\#1963](https://github.com/googleapis/java-datastore/issues/1963) ) ( [833a34a](https://github.com/googleapis/java-datastore/commit/833a34a7e5ab1194d2ac8ebf097d7c300d7e8d37) )

## September 02, 2025

Feature

Use [Query insights](/datastore/docs/query-insights) to view query performance metrics for your database. This feature is now generally available ( [GA](https://cloud.google.com/products#product-launch-stages) ).

## August 25, 2025

Libraries

### Java

#### [2.31.3](https://github.com/googleapis/java-datastore/compare/v2.31.2...v2.31.3) (2025-08-20)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.52.0 ( [\#1944](https://github.com/googleapis/java-datastore/issues/1944) ) ( [30a6e28](https://github.com/googleapis/java-datastore/commit/30a6e2856ee87568f14bbe94fe5918a4ecea4612) )

### Java

#### [2.31.4](https://github.com/googleapis/java-datastore/compare/v2.31.3...v2.31.4) (2025-08-22)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.62.0 ( [90f5526](https://github.com/googleapis/java-datastore/commit/90f552624627b3ca6fde4b4241b66893019174dd) )

## August 18, 2025

Libraries

### Java

#### [2.31.2](https://github.com/googleapis/java-datastore/compare/v2.31.1...v2.31.2) (2025-08-08)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.61.0 ( [c7bd68d](https://github.com/googleapis/java-datastore/commit/c7bd68de82ec06f06c41cd12e87cc96a337dcd02) )

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.51.0 ( [\#1936](https://github.com/googleapis/java-datastore/issues/1936) ) ( [a25433f](https://github.com/googleapis/java-datastore/commit/a25433f805f957dc0beebaeef466aa20f14f8ccc) )

## August 04, 2025

Libraries

### Java

#### [2.31.1](https://github.com/googleapis/java-datastore/compare/v2.31.0...v2.31.1) (2025-07-28)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.60.2 ( [06372cd](https://github.com/googleapis/java-datastore/commit/06372cd63a7ce35747d90c62cc1d57be0a6ffb37) )

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.50.2 ( [\#1926](https://github.com/googleapis/java-datastore/issues/1926) ) ( [1ecdf37](https://github.com/googleapis/java-datastore/commit/1ecdf377b2a6ccb2ffd231744726807b0493df79) )

## August 01, 2025

Feature

You can [clone an existing database](/datastore/docs/manage-databases#clone-database) at a selected timestamp into a new database. This feature is available in [Preview](https://cloud.google.com/products#product-launch-stages) .

## July 21, 2025

Libraries

### Java

#### [2.31.0](https://github.com/googleapis/java-datastore/compare/v2.30.0...v2.31.0) (2025-07-14)

##### Features

  - Next release from main branch is 2.31.0 ( [\#1912](https://github.com/googleapis/java-datastore/issues/1912) ) ( [a74c46b](https://github.com/googleapis/java-datastore/commit/a74c46bfbac8eaf5c97fe653b740e26e7c79f4da) )

##### Dependencies

  - Update dependency com.google.cloud:gapic-libraries-bom to v1.61.0 ( [\#1901](https://github.com/googleapis/java-datastore/issues/1901) ) ( [beeb125](https://github.com/googleapis/java-datastore/commit/beeb125efc842776facfa67742bdf8b6c167e9f2) )
  - Update dependency com.google.cloud:sdk-platform-java-config to v3.50.1 ( [\#1908](https://github.com/googleapis/java-datastore/issues/1908) ) ( [b10e0f0](https://github.com/googleapis/java-datastore/commit/b10e0f0748decf06574fc0eb7ddba33ee5ece1a7) )

## June 30, 2025

Libraries

### Java

#### [2.30.0](https://github.com/googleapis/java-datastore/compare/v2.29.2...v2.30.0) (2025-06-26)

##### Features

  - Enable grpc configurator for client-side tracing ( [\#1886](https://github.com/googleapis/java-datastore/issues/1886) ) ( [97004c8](https://github.com/googleapis/java-datastore/commit/97004c85d73541ccfc26e0f4212e3a447d3e4ba6) )

##### Dependencies

  - Update dependency com.google.cloud:gapic-libraries-bom to v1.60.0 ( [\#1799](https://github.com/googleapis/java-datastore/issues/1799) ) ( [bf2a33c](https://github.com/googleapis/java-datastore/commit/bf2a33c32a04b978a19fd6dfbe845769c921fa4f) )
  - Update dependency com.google.cloud:sdk-platform-java-config to v3.50.0 ( [\#1897](https://github.com/googleapis/java-datastore/issues/1897) ) ( [a8d99cd](https://github.com/googleapis/java-datastore/commit/a8d99cde26c38376b596f44379f4d069b25339b2) )
  - Update googleapis/sdk-platform-java action to v2.59.1 ( [\#1880](https://github.com/googleapis/java-datastore/issues/1880) ) ( [4fb9929](https://github.com/googleapis/java-datastore/commit/4fb992943152bb4533e0bbd80e373de61f5ec864) )
  - Update googleapis/sdk-platform-java action to v2.60.0 ( [\#1898](https://github.com/googleapis/java-datastore/issues/1898) ) ( [0921f86](https://github.com/googleapis/java-datastore/commit/0921f869ff4a19e7c0fe918aea0896922e9a18af) )

## June 16, 2025

Libraries

### Java

#### [2.29.2](https://github.com/googleapis/java-datastore/compare/v2.29.1...v2.29.2) (2025-06-13)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.59.0 ( [910a6c2](https://github.com/googleapis/java-datastore/commit/910a6c20cb23f441ede5cd75972c65adbb8752e8) )

## June 09, 2025

Libraries

### Java

#### [2.29.0](https://github.com/googleapis/java-datastore/compare/v2.28.2...v2.29.0) (2025-06-06)

##### Features

  - Add getNumber to AggregationResult (https://github.com/googleapis/java-datastore/issues/1851) ( [\#1861](https://github.com/googleapis/java-datastore/issues/1861) ) ( [b9c2c3f](https://github.com/googleapis/java-datastore/commit/b9c2c3ff775f7123d701ccacff9bd2ea3718243b) )

##### Bug Fixes

  - Remove 500 char path name limit ( [\#1865](https://github.com/googleapis/java-datastore/issues/1865) ) ( [1097175](https://github.com/googleapis/java-datastore/commit/10971752310d8b1794c8e77041b582707142b328) )

##### Dependencies

  - Update dependency org.easymock:easymock to v5.6.0 ( [\#1858](https://github.com/googleapis/java-datastore/issues/1858) ) ( [acc1513](https://github.com/googleapis/java-datastore/commit/acc1513ad90e8da6743e618322bae075bac4ac46) )

### Java

#### [2.29.1](https://github.com/googleapis/java-datastore/compare/v2.29.0...v2.29.1) (2025-06-07)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.49.0 ( [\#1860](https://github.com/googleapis/java-datastore/issues/1860) ) ( [0eff028](https://github.com/googleapis/java-datastore/commit/0eff0284bf78152341e1692ffc57930f62ec01dc) )

## May 26, 2025

Libraries

### Java

#### [2.28.2](https://github.com/googleapis/java-datastore/compare/v2.28.1...v2.28.2) (2025-05-16)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.48.0 ( [\#1847](https://github.com/googleapis/java-datastore/issues/1847) ) ( [7ed3232](https://github.com/googleapis/java-datastore/commit/7ed32321a5c84c4b2f61094e4c4adb5e36e5bc1b) )
  - Update googleapis/sdk-platform-java action to v2.58.0 ( [\#1853](https://github.com/googleapis/java-datastore/issues/1853) ) ( [eef820d](https://github.com/googleapis/java-datastore/commit/eef820d017f5e00245924d551abe172a2a39e29f) )

## May 12, 2025

Libraries

### Java

#### [2.28.1](https://github.com/googleapis/java-datastore/compare/v2.28.0...v2.28.1) (2025-05-06)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.47.0 ( [\#1841](https://github.com/googleapis/java-datastore/issues/1841) ) ( [ac393e6](https://github.com/googleapis/java-datastore/commit/ac393e61e517d30b534be3e99070c210081c4f0b) )
  - Update googleapis/sdk-platform-java action to v2.57.0 ( [\#1842](https://github.com/googleapis/java-datastore/issues/1842) ) ( [0745906](https://github.com/googleapis/java-datastore/commit/0745906bbdd8819ac2ccaafa301c8f4b4fd20be4) )

## May 05, 2025

Libraries

### Java

#### [2.28.0](https://github.com/googleapis/java-datastore/compare/v2.27.2...v2.28.0) (2025-04-29)

##### Features

  - Java datastore gapic upgrade ( [\#1824](https://github.com/googleapis/java-datastore/issues/1824) ) ( [a296d43](https://github.com/googleapis/java-datastore/commit/a296d43724c57aba6a69ebed249261e3d367d625) )

## April 28, 2025

Libraries

### Java

#### [2.27.2](https://github.com/googleapis/java-datastore/compare/v2.27.1...v2.27.2) (2025-04-25)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.56.2 ( [1210f32](https://github.com/googleapis/java-datastore/commit/1210f32662e7aafd2e170643bedbb851f40f3646) )

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.46.2 ( [\#1823](https://github.com/googleapis/java-datastore/issues/1823) ) ( [4d2026c](https://github.com/googleapis/java-datastore/commit/4d2026c330009becc201a95c42af365cc83b8ea5) )

## April 22, 2025

Feature

Committed use discounts are now [generally available (GA)](https://cloud.google.com/products#product-launch-stages) for Firestore in Datastore mode in exchange for a commitment to continuously spend a certain amount on read/write/delete operations for one year or three years. For details, see [Committed use discounts](/datastore/docs/cuds) .

## April 21, 2025

Libraries

### Python

#### [2.21.0](https://github.com/googleapis/python-datastore/compare/v2.20.2...v2.21.0) (2025-04-10)

##### Features

  - Add REST Interceptors which support reading metadata ( [7be9c4c](https://github.com/googleapis/python-datastore/commit/7be9c4c594af2c2414e394b8bfe62574b58ef337) )
  - Add support for opt-in debug logging ( [7be9c4c](https://github.com/googleapis/python-datastore/commit/7be9c4c594af2c2414e394b8bfe62574b58ef337) )

##### Bug Fixes

  - Allow protobuf 6.x ( [\#598](https://github.com/googleapis/python-datastore/issues/598) ) ( [7c1171b](https://github.com/googleapis/python-datastore/commit/7c1171bf657f7cf4d1404e19611f6c874a8998ca) )
  - Backwards-compatibility for previous meaning format ( [\#603](https://github.com/googleapis/python-datastore/issues/603) ) ( [ed92e8e](https://github.com/googleapis/python-datastore/commit/ed92e8e54a9e0f44302efee89a30a322d0a73636) )
  - Fix typing issue with gRPC metadata when key ends in -bin ( [7be9c4c](https://github.com/googleapis/python-datastore/commit/7be9c4c594af2c2414e394b8bfe62574b58ef337) )

## April 09, 2025

Feature

You can now use Query insights to [view query performance metrics for your database](/datastore/docs/query-insights) . This feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

## March 24, 2025

Feature

Firestore in Datastore mode now supports multi-region `  nam7  ` United States (Central and East), which consists of regions `  us-central1  ` (Iowa) and `  us-east4  ` (Northern Virginia).

For a full list of supported locations, see [Locations](/firestore/docs/locations) .

Libraries

### Java

#### [2.27.1](https://github.com/googleapis/java-datastore/compare/v2.27.0...v2.27.1) (2025-03-18)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.55.1 ( [ba1ad98](https://github.com/googleapis/java-datastore/commit/ba1ad98cce4c0feae13a370ea0581d15674dd43c) )

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.45.1 ( [\#1791](https://github.com/googleapis/java-datastore/issues/1791) ) ( [ab5ac8e](https://github.com/googleapis/java-datastore/commit/ab5ac8e6407541520fabb4504fcce0d675347f63) )

## March 10, 2025

Libraries

### Java

#### [2.27.0](https://github.com/googleapis/java-datastore/compare/v2.26.4...v2.27.0) (2025-03-05)

##### Features

  - Next release from main branch is 2.27.0 ( [\#1781](https://github.com/googleapis/java-datastore/issues/1781) ) ( [d29f47c](https://github.com/googleapis/java-datastore/commit/d29f47cbef9998acdc8b7b0f42d93574dab3cc7f) )

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.54.0 ( [b9b302b](https://github.com/googleapis/java-datastore/commit/b9b302bb6c8bb1c8d8b175b776b2f65317511987) )

##### Dependencies

  - Update dependency com.google.cloud:gapic-libraries-bom to v1.53.0 ( [\#1779](https://github.com/googleapis/java-datastore/issues/1779) ) ( [8369118](https://github.com/googleapis/java-datastore/commit/8369118994e9a18b888a7779376fea7e22b219ed) )

## March 04, 2025

Feature

Firestore in Datastore mode now supports the `  europe-north2  ` Stockholm region.

For a full list of supported locations, see [Locations](/datastore/docs/locations) .

## March 03, 2025

Libraries

### Java

#### [2.26.4](https://github.com/googleapis/java-datastore/compare/v2.26.3...v2.26.4) (2025-02-26)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.44.0 ( [\#1769](https://github.com/googleapis/java-datastore/issues/1769) ) ( [7a86509](https://github.com/googleapis/java-datastore/commit/7a8650939e652fc3b384053454d6ef5084bb1508) )

## February 24, 2025

Libraries

### Java

#### [2.26.3](https://github.com/googleapis/java-datastore/compare/v2.26.2...v2.26.3) (2025-02-21)

##### Dependencies

  - Update dependency com.google.cloud:gapic-libraries-bom to v1.52.0 ( [\#1747](https://github.com/googleapis/java-datastore/issues/1747) ) ( [592072b](https://github.com/googleapis/java-datastore/commit/592072b194706e63a7fd4a6f6230377e8f4b729d) )

## February 17, 2025

Libraries

### Java

#### [2.26.2](https://github.com/googleapis/java-datastore/compare/v2.26.1...v2.26.2) (2025-02-12)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.53.0 ( [be0d0cd](https://github.com/googleapis/java-datastore/commit/be0d0cd960b9254d26404d9331b78dee1104cf0a) )

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.43.0 ( [\#1737](https://github.com/googleapis/java-datastore/issues/1737) ) ( [7272a41](https://github.com/googleapis/java-datastore/commit/7272a4197a0d7fb97ee039ccb88ac13a1ec037d1) )
  - Update googleapis/sdk-platform-java action to v2.53.0 ( [\#1738](https://github.com/googleapis/java-datastore/issues/1738) ) ( [b8a7a5d](https://github.com/googleapis/java-datastore/commit/b8a7a5d5d8700ccccb643162843e3043396a9444) )

## February 10, 2025

Libraries

### Java

#### [2.26.1](https://github.com/googleapis/java-datastore/compare/v2.26.0...v2.26.1) (2025-02-05)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.52.0 ( [9594024](https://github.com/googleapis/java-datastore/commit/95940241de9f324000d52dc80b3106aedefd481e) )

##### Dependencies

  - Update dependency com.google.cloud:gapic-libraries-bom to v1.51.0 ( [\#1726](https://github.com/googleapis/java-datastore/issues/1726) ) ( [89f31a8](https://github.com/googleapis/java-datastore/commit/89f31a88d346193c9a5533de3e38c9088db30043) )

## February 03, 2025

Libraries

### Java

#### [2.26.0](https://github.com/googleapis/java-datastore/compare/v2.25.4...v2.26.0) (2025-01-29)

##### Features

  - Add firestoreInDatastoreMode for datastore emulator ( [\#1698](https://github.com/googleapis/java-datastore/issues/1698) ) ( [50f106d](https://github.com/googleapis/java-datastore/commit/50f106d4c50884ce471a66c00df322270fe4a91c) )

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.42.0 ( [\#1725](https://github.com/googleapis/java-datastore/issues/1725) ) ( [1cbaf22](https://github.com/googleapis/java-datastore/commit/1cbaf22cf557aec606dce7a5ca5d3ebe620a9339) )

## January 27, 2025

Libraries

### Java

#### [2.25.4](https://github.com/googleapis/java-datastore/compare/v2.25.3...v2.25.4) (2025-01-22)

##### Dependencies

  - Update dependency org.easymock:easymock to v5.5.0 ( [\#1666](https://github.com/googleapis/java-datastore/issues/1666) ) ( [0333b07](https://github.com/googleapis/java-datastore/commit/0333b0744bab87afe78dad1c17f6811d3dec47e6) )

## January 20, 2025

Libraries

### Java

#### [2.25.3](https://github.com/googleapis/java-datastore/compare/v2.25.2...v2.25.3) (2025-01-15)

##### Dependencies

  - Update dependency com.google.cloud:gapic-libraries-bom to v1.50.0 ( [\#1708](https://github.com/googleapis/java-datastore/issues/1708) ) ( [b78660f](https://github.com/googleapis/java-datastore/commit/b78660f3866ce5c1198db4590b5e1f645170ecff) )

## January 13, 2025

Libraries

### Java

#### [2.25.2](https://github.com/googleapis/java-datastore/compare/v2.25.1...v2.25.2) (2025-01-09)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.51.1 ( [90d8b30](https://github.com/googleapis/java-datastore/commit/90d8b3034d5a583d880a822d1e763035a2120f4a) )
  - Fix emulator command arg data-dir ( [\#1695](https://github.com/googleapis/java-datastore/issues/1695) ) ( [9d53195](https://github.com/googleapis/java-datastore/commit/9d531957da3f017f0702a126601eaa8afe3113d6) )

##### Dependencies

  - Update dependency com.google.cloud:gapic-libraries-bom to v1.49.0 ( [\#1693](https://github.com/googleapis/java-datastore/issues/1693) ) ( [8160c28](https://github.com/googleapis/java-datastore/commit/8160c2895e947c118cea24e92d9a31a1fdf4653f) )
  - Update dependency com.google.cloud:sdk-platform-java-config to v3.41.1 ( [\#1703](https://github.com/googleapis/java-datastore/issues/1703) ) ( [bf9537f](https://github.com/googleapis/java-datastore/commit/bf9537f81b6e7cc2252ad0183fb87db656b009d7) )
  - Update dependency com.google.guava:guava-testlib to v33.4.0-jre ( [\#1694](https://github.com/googleapis/java-datastore/issues/1694) ) ( [b91a2af](https://github.com/googleapis/java-datastore/commit/b91a2af534eb7568ec86a0b27a80a6bd2943af7b) )

## December 16, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.20.2](https://github.com/googleapis/python-datastore/compare/v2.20.1...v2.20.2) (2024-12-12)

##### Bug Fixes

  - Preserve list meanings ( [\#575](https://github.com/googleapis/python-datastore/issues/575) ) ( [266243b](https://github.com/googleapis/python-datastore/commit/266243ba360a9d41ab4b51c323eac44d2cfc35cb) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.25.1](https://github.com/googleapis/java-datastore/compare/v2.25.0...v2.25.1) (2024-12-13)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.51.0 ( [106ee4d](https://github.com/googleapis/java-datastore/commit/106ee4dd7ca4dd9e59a5419f59b8625680e60f15) )

##### Dependencies

  - Update sdk platform java dependencies ( [\#1685](https://github.com/googleapis/java-datastore/issues/1685) ) ( [4372350](https://github.com/googleapis/java-datastore/commit/4372350117ba57903f510512a383339b6a4ea47c) )

#### [2.25.0](https://github.com/googleapis/java-datastore/compare/v2.24.3...v2.25.0) (2024-12-11)

##### Features

  - Introduce `  java.time  ` methods and variables ( [\#1671](https://github.com/googleapis/java-datastore/issues/1671) ) ( [5a78a80](https://github.com/googleapis/java-datastore/commit/5a78a8075867f4b2fc598f0423bd2ab65b559856) )

##### Dependencies

  - Update dependency com.google.cloud:gapic-libraries-bom to v1.48.0 ( [\#1605](https://github.com/googleapis/java-datastore/issues/1605) ) ( [5c6a678](https://github.com/googleapis/java-datastore/commit/5c6a67844f7b5d4c7001cccd1bed3d0d56be6e90) )

##### Documentation

  - Update gapic upgrade installation instructions ( [\#1677](https://github.com/googleapis/java-datastore/issues/1677) ) ( [b3fbfcc](https://github.com/googleapis/java-datastore/commit/b3fbfcc9654bc63bf0d8f3025641d8c50a24ef97) )

## November 25, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.24.3](https://github.com/googleapis/java-datastore/compare/v2.24.2...v2.24.3) (2024-11-18)

##### Dependencies

  - Update sdk platform java dependencies ( [\#1662](https://github.com/googleapis/java-datastore/issues/1662) ) ( [b4d3ab9](https://github.com/googleapis/java-datastore/commit/b4d3ab9a72bb2a4dff59bf54abcc5d9536b2596b) )

## November 22, 2024

Feature

You can now use Active Assist to provide recommendations and insights that improve the reliability of your databases. This feature is generally available (GA).

For more information, see [Reliability recommender](/datastore/docs/reliability-recommender) .

## November 18, 2024

Feature

Firestore in Datastore mode now supports the `  northamerica-south1  ` Queretaro region.

For a full list of supported locations, see [Locations](/datastore/docs/locations) .

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.24.2](https://github.com/googleapis/java-datastore/compare/v2.24.1...v2.24.2) (2024-11-06)

##### Bug Fixes

  - **doc:** Add discriptions for TransactionCallable interface ( [\#1644](https://github.com/googleapis/java-datastore/issues/1644) ) ( [173a883](https://github.com/googleapis/java-datastore/commit/173a88330cc5693f54504348cf39bf3191db2250) )
  - **doc:** Fix return types for batch interface ( [\#1645](https://github.com/googleapis/java-datastore/issues/1645) ) ( [1189211](https://github.com/googleapis/java-datastore/commit/11892116f0fb8eacb711a8f48e780e48a232f987) )

## November 11, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [9.2.1](https://github.com/googleapis/nodejs-datastore/compare/v9.2.0...v9.2.1) (2024-11-06)

##### Bug Fixes

  - Address edge cases for excluding large properties when using save ( [\#1356](https://github.com/googleapis/nodejs-datastore/issues/1356) ) ( [ceaff7e](https://github.com/googleapis/nodejs-datastore/commit/ceaff7ef468413ff10e03e0b3ed923b4b5a37a08) )
  - Create a release ( [\#1353](https://github.com/googleapis/nodejs-datastore/issues/1353) ) ( [536873e](https://github.com/googleapis/nodejs-datastore/commit/536873e24bacc9477f1a9c4c5403ed08d5c8cc93) )

## November 06, 2024

Feature

You can now use the managed bulk delete service to delete entities in bulk. This feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

For more information, see [Bulk delete data](/datastore/docs/bulk-delete) .

## November 04, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [9.2.0](https://github.com/googleapis/nodejs-datastore/compare/v9.1.0...v9.2.0) (2024-10-30)

##### Features

  - Add FindNearest API to the stable branch ( [\#1333](https://github.com/googleapis/nodejs-datastore/issues/1333) ) ( [1d56433](https://github.com/googleapis/nodejs-datastore/commit/1d5643369226c5fc220779f4c90fa804d8f876af) )
  - Update Go Datastore import path ( [\#1261](https://github.com/googleapis/nodejs-datastore/issues/1261) ) ( [bf3dafd](https://github.com/googleapis/nodejs-datastore/commit/bf3dafd8267c447a52f7764505042a60b1a9fd28) )

##### Bug Fixes

  - Add excludeFromIndexes in the proper places for large properties of nested fields ( [\#1266](https://github.com/googleapis/nodejs-datastore/issues/1266) ) ( [9c7730a](https://github.com/googleapis/nodejs-datastore/commit/9c7730a35699be049beeac0c4bb469239971d471) )
  - Query object description ( [\#1340](https://github.com/googleapis/nodejs-datastore/issues/1340) ) ( [ad2c6c0](https://github.com/googleapis/nodejs-datastore/commit/ad2c6c01b83f0ae42a3dc4268feb5f4b45890f7c) )

### Go

### Changes for [datastore/admin/apiv1](https://github.com/googleapis/google-cloud-go/tree/main/datastore/admin/apiv1)

#### [1.20.0](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.19.0...datastore/v1.20.0) (2024-10-29)

##### Features

  - **datastore:** Add FindNearest API to the stable branch ( [\#10980](https://github.com/googleapis/google-cloud-go/issues/10980) ) ( [f0b05e2](https://github.com/googleapis/google-cloud-go/commit/f0b05e260435d5e8889b9a0ca0ab215fcde169ab) )
  - **datastore:** Support for field update operators in the Datastore API and resolution strategies when there is a conflict at write time ( [78d8513](https://github.com/googleapis/google-cloud-go/commit/78d8513f7e31c6ef118bdfc784049b8c7f1e3249) )

##### Bug Fixes

  - **datastore:** Bump dependencies ( [2ddeb15](https://github.com/googleapis/google-cloud-go/commit/2ddeb1544a53188a7592046b98913982f1b0cf04) )
  - **datastore:** Do not delay on final transaction attempt ( [\#10824](https://github.com/googleapis/google-cloud-go/issues/10824) ) ( [0d732cc](https://github.com/googleapis/google-cloud-go/commit/0d732cc87b432589f156c96d430e13c792dceeeb) )
  - **datastore:** Remove namespace from Key.String() ( [40229e6](https://github.com/googleapis/google-cloud-go/commit/40229e65f574d63e2f31e5b15ec61d565db59fef) )
  - **datastore:** Remove namespace from Key.String() ( [\#10684](https://github.com/googleapis/google-cloud-go/issues/10684) ) ( [\#10823](https://github.com/googleapis/google-cloud-go/issues/10823) ) ( [40229e6](https://github.com/googleapis/google-cloud-go/commit/40229e65f574d63e2f31e5b15ec61d565db59fef) )
  - **datastore:** Update google.golang.org/api to v0.203.0 ( [8bb87d5](https://github.com/googleapis/google-cloud-go/commit/8bb87d56af1cba736e0fe243979723e747e5e11e) )
  - **datastore:** Use local retryer in transactions ( [\#11050](https://github.com/googleapis/google-cloud-go/issues/11050) ) ( [3ef61a2](https://github.com/googleapis/google-cloud-go/commit/3ef61a29f10d34355d44830b5d473cacd6cf2be5) )
  - **datastore:** WARNING: On approximately Dec 1, 2024, an update to Protobuf will change service registration function signatures to use an interface instead of a concrete type in generated .pb.go files. This change is expected to affect very few if any users of this client library. For more information, see https://togithub.com/googleapis/google-cloud-go/issues/11020. ( [8bb87d5](https://github.com/googleapis/google-cloud-go/commit/8bb87d56af1cba736e0fe243979723e747e5e11e) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.24.1](https://github.com/googleapis/java-datastore/compare/v2.24.0...v2.24.1) (2024-10-28)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.39.0 ( [\#1640](https://github.com/googleapis/java-datastore/issues/1640) ) ( [fe61f66](https://github.com/googleapis/java-datastore/commit/fe61f6691a5e3c8fbfc974b6fe613a69652241ca) )
  - Update googleapis/sdk-platform-java action to v2.49.0 ( [\#1638](https://github.com/googleapis/java-datastore/issues/1638) ) ( [57598d7](https://github.com/googleapis/java-datastore/commit/57598d7d59cd6917f23a653403613e4edc160c64) )

## October 28, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.24.0](https://github.com/googleapis/java-datastore/compare/v2.23.0...v2.24.0) (2024-10-24)

##### Features

  - Add FindNearest API to the stable branch ( [3512ba2](https://github.com/googleapis/java-datastore/commit/3512ba2f1bcd358e3c39c36944e05873b3f25f51) )

##### Bug Fixes

  - **sample:** Change update entity sample to use transaction ( [\#1633](https://github.com/googleapis/java-datastore/issues/1633) ) ( [c44f17a](https://github.com/googleapis/java-datastore/commit/c44f17a7bb93d688367611ee2533c59c940ae61f) )

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.38.0 ( [\#1632](https://github.com/googleapis/java-datastore/issues/1632) ) ( [6453f1e](https://github.com/googleapis/java-datastore/commit/6453f1e44f370a13434ef68295ae5638612032c8) )
  - Update googleapis/sdk-platform-java action to v2.48.0 ( [\#1628](https://github.com/googleapis/java-datastore/issues/1628) ) ( [d3bce79](https://github.com/googleapis/java-datastore/commit/d3bce79467254b3128a8f16d5754e91d29ece525) )

## October 21, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.23.0](https://github.com/googleapis/java-datastore/compare/v2.22.0...v2.23.0) (2024-10-14)

##### Features

  - Support for field update operators in the Datastore API and resolution strategies when there is a conflict at write time ( [b299266](https://github.com/googleapis/java-datastore/commit/b299266e42037b731ee7bbba21dbded73a37323c) )

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.46.1 ( [678eee2](https://github.com/googleapis/java-datastore/commit/678eee2dfb6d447a852edd436137f8ebfbe50d74) )
  - **deps:** Update the Java code generator (gapic-generator-java) to 2.47.0 ( [b299266](https://github.com/googleapis/java-datastore/commit/b299266e42037b731ee7bbba21dbded73a37323c) )

##### Dependencies

  - Update sdk platform java dependencies ( [\#1617](https://github.com/googleapis/java-datastore/issues/1617) ) ( [6eaff23](https://github.com/googleapis/java-datastore/commit/6eaff23f9de25ae6ad2a4fea67c0b65a243c08fd) )

## October 07, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.22.0](https://github.com/googleapis/java-datastore/compare/v2.21.3...v2.22.0) (2024-09-26)

##### Features

  - Add sample code for multiple inequalities indexing consideration query ( [\#1579](https://github.com/googleapis/java-datastore/issues/1579) ) ( [1286792](https://github.com/googleapis/java-datastore/commit/1286792d7b49229d698df652cd117d229a5cd97e) )
  - Introducing Tracing with OpenTelemetry API [\#1537](https://github.com/googleapis/java-datastore/issues/1537) ( [\#1576](https://github.com/googleapis/java-datastore/issues/1576) ) ( [5440c22](https://github.com/googleapis/java-datastore/commit/5440c22364074c108450c3a748a6a17d5f1dddda) )

##### Bug Fixes

  - Update opentelemetry-sdk dependency to be test-only ( [\#1595](https://github.com/googleapis/java-datastore/issues/1595) ) ( [9d719e8](https://github.com/googleapis/java-datastore/commit/9d719e809ea830d8602399b72e432580f14ae6bd) )
  - Update opentelemetry.version to 1.42.1 to match the BOM version ( [\#1598](https://github.com/googleapis/java-datastore/issues/1598) ) ( [23c5c26](https://github.com/googleapis/java-datastore/commit/23c5c2662117370c66c611604c56b878d41f4738) )

##### Dependencies

  - Update dependency com.google.cloud:gapic-libraries-bom to v1.43.0 ( [\#1584](https://github.com/googleapis/java-datastore/issues/1584) ) ( [fae3b74](https://github.com/googleapis/java-datastore/commit/fae3b74eaa3494a27fd43f56435c01e8fc09e5ee) )
  - Update dependency com.google.cloud:sdk-platform-java-config to v3.36.0 ( [\#1590](https://github.com/googleapis/java-datastore/issues/1590) ) ( [2db9e43](https://github.com/googleapis/java-datastore/commit/2db9e439189baf8f97127f6cff1de5d47efb0073) )
  - Update dependency com.google.cloud:sdk-platform-java-config to v3.36.1 ( [\#1602](https://github.com/googleapis/java-datastore/issues/1602) ) ( [e1b7d4b](https://github.com/googleapis/java-datastore/commit/e1b7d4b205312d7d4c2a285f3d1f61388da65c83) )
  - Update dependency com.google.guava:guava-testlib to v33.3.1-jre ( [\#1592](https://github.com/googleapis/java-datastore/issues/1592) ) ( [5d078a4](https://github.com/googleapis/java-datastore/commit/5d078a4b294d071716f51f0d4b9baa5d65a0fe90) )
  - Update dependency com.google.testparameterinjector:test-parameter-injector to v1.17 ( [\#1585](https://github.com/googleapis/java-datastore/issues/1585) ) ( [8f74a49](https://github.com/googleapis/java-datastore/commit/8f74a49c5982d00bd168e78671163683f7b41126) )

## October 02, 2024

Feature

You can now use [property transforms like `  increment  `](/datastore/docs/concepts/entities#property_transforms) in the REST API. This feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

## October 01, 2024

Feature

The Java client library for Firestore in Datastore mode [now supports client-side tracing](/datastore/docs/client-side-traces) . This feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

Feature

You can now use customer-managed encryption keys (CMEK) in Datastore to protect your data. This feature is generally available (GA) behind an allow-list.

For more information, see [Customer-managed encryption keys (CMEK)](/datastore/docs/cmek) .

## September 16, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.21.3](https://github.com/googleapis/java-datastore/compare/v2.21.2...v2.21.3) (2024-09-11)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.35.0 ( [\#1561](https://github.com/googleapis/java-datastore/issues/1561) ) ( [5a79fd8](https://github.com/googleapis/java-datastore/commit/5a79fd8d1202e65c02423fe40402c41af6050efa) )
  - Update dependency com.google.errorprone:error\_prone\_core to v2.31.0 ( [\#1523](https://github.com/googleapis/java-datastore/issues/1523) ) ( [8d3af32](https://github.com/googleapis/java-datastore/commit/8d3af322fb56032cd7a9d29e60fd93d1f3e7e632) )
  - Update dependency com.google.guava:guava-testlib to v33.3.0-jre ( [\#1548](https://github.com/googleapis/java-datastore/issues/1548) ) ( [18ba37f](https://github.com/googleapis/java-datastore/commit/18ba37f60b5b3e69c95f6e55a28daf8c0de82ba9) )
  - Update dependency org.easymock:easymock to v5.4.0 ( [\#1482](https://github.com/googleapis/java-datastore/issues/1482) ) ( [ee788a1](https://github.com/googleapis/java-datastore/commit/ee788a162841994e09a61bb81b94cbe93353a78e) )

## September 09, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-ndb](https://github.com/googleapis/python-ndb)

#### [2.3.2](https://github.com/googleapis/python-ndb/compare/v2.3.1...v2.3.2) (2024-07-15)

##### Bug Fixes

  - Allow Protobuf 5.x ( [\#991](https://github.com/googleapis/python-ndb/issues/991) ) ( [5812a3c](https://github.com/googleapis/python-ndb/commit/5812a3c2833ef9edda1726645e32789752474bd6) )

## August 26, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Go

### Changes for [datastore/admin/apiv1](https://github.com/googleapis/google-cloud-go/tree/main/datastore/admin/apiv1)

#### [1.19.0](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.18.0...datastore/v1.19.0) (2024-08-22)

##### Features

  - **datastore:** Reference new protos ( [\#10724](https://github.com/googleapis/google-cloud-go/issues/10724) ) ( [d8887df](https://github.com/googleapis/google-cloud-go/commit/d8887df4a12fe56606515c116fe1db12a6549aa1) )

#### [1.18.0](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.17.1...datastore/v1.18.0) (2024-08-21)

##### Features

  - **datastore:** Add support for Go 1.23 iterators ( [84461c0](https://github.com/googleapis/google-cloud-go/commit/84461c0ba464ec2f951987ba60030e37c8a8fc18) )
  - **datastore:** Start generating datastorepb protos ( [946a5fc](https://github.com/googleapis/google-cloud-go/commit/946a5fcfeb85e22b1d8e995cda6b18b745459656) )

##### Bug Fixes

  - **datastore:** Bump google.golang.org/api@v0.187.0 ( [8fa9e39](https://github.com/googleapis/google-cloud-go/commit/8fa9e398e512fd8533fd49060371e61b5725a85b) )
  - **datastore:** Bump google.golang.org/grpc@v1.64.1 ( [8ecc4e9](https://github.com/googleapis/google-cloud-go/commit/8ecc4e9622e5bbe9b90384d5848ab816027226c5) )
  - **datastore:** Ignore field mismatch errors ( [\#8694](https://github.com/googleapis/google-cloud-go/issues/8694) ) ( [6625d12](https://github.com/googleapis/google-cloud-go/commit/6625d12c3135587f188cc8f801beb9ae5a0c7515) )
  - **datastore:** Update dependencies ( [257c40b](https://github.com/googleapis/google-cloud-go/commit/257c40bd6d7e59730017cf32bda8823d7a232758) )
  - **datastore:** Update google.golang.org/api to v0.191.0 ( [5b32644](https://github.com/googleapis/google-cloud-go/commit/5b32644eb82eb6bd6021f80b4fad471c60fb9d73) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.21.2](https://github.com/googleapis/java-datastore/compare/v2.21.1...v2.21.2) (2024-08-22)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.34.0 ( [\#1547](https://github.com/googleapis/java-datastore/issues/1547) ) ( [8c5f595](https://github.com/googleapis/java-datastore/commit/8c5f5954d88732ab929b4477a3f15b0052adc2ff) )

## August 19, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.20.1](https://github.com/googleapis/python-datastore/compare/v2.20.0...v2.20.1) (2024-08-14)

##### Bug Fixes

  - Allow protobuf 5.x; require protobuf \>=3.20.2 ( [\#560](https://github.com/googleapis/python-datastore/issues/560) ) ( [ad50e36](https://github.com/googleapis/python-datastore/commit/ad50e3648954edf27575001be833bb5e1e598f46) )

## August 12, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.20.0](https://github.com/googleapis/python-datastore/compare/v2.19.0...v2.20.0) (2024-08-07)

##### Features

  - Add new types ExplainOptions, ExplainMetrics, PlanSummary, ExecutionStats ( [\#521](https://github.com/googleapis/python-datastore/issues/521) ) ( [dfbee2d](https://github.com/googleapis/python-datastore/commit/dfbee2db800a3ca99e65a5d386ea907db1c46598) )
  - Add new\_transaction support ( [\#499](https://github.com/googleapis/python-datastore/issues/499) ) ( [43855dd](https://github.com/googleapis/python-datastore/commit/43855dd1762f51771bb1a3924c6a234641950fb6) )
  - Implement query profiling ( [\#542](https://github.com/googleapis/python-datastore/issues/542) ) ( [1500f70](https://github.com/googleapis/python-datastore/commit/1500f7007f251256ce2923e1168439d40d41cc4d) )
  - New PropertyMask field which allows partial commits, lookups, and query results ( [7fd218b](https://github.com/googleapis/python-datastore/commit/7fd218b2afc0282d8fea21992e8d10c5eec72ac7) )

##### Bug Fixes

  - Retry and timeout values do not propagate in requests during pagination ( [\#555](https://github.com/googleapis/python-datastore/issues/555) ) ( [5e773cb](https://github.com/googleapis/python-datastore/commit/5e773cb8c766303fef53965dd100b3c4c93b98be) )
  - Using end\_cursor instead of skipped\_cursor in Iterator to fix rare bug. ( [\#552](https://github.com/googleapis/python-datastore/issues/552) ) ( [4982f9a](https://github.com/googleapis/python-datastore/commit/4982f9a6cbbe2de449535295a363a2dd49538c86) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.21.1](https://github.com/googleapis/java-datastore/compare/v2.21.0...v2.21.1) (2024-08-06)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.33.0 ( [\#1531](https://github.com/googleapis/java-datastore/issues/1531) ) ( [9e52395](https://github.com/googleapis/java-datastore/commit/9e52395f7ee71315331790284d35e7aad2f387ed) )

#### [2.21.0](https://github.com/googleapis/java-datastore/compare/v2.20.2...v2.21.0) (2024-07-31)

##### Features

  - Enable hermetic library generation ( [\#1462](https://github.com/googleapis/java-datastore/issues/1462) ) ( [d142d9c](https://github.com/googleapis/java-datastore/commit/d142d9c95d91c8cadaf696efc12d6136814938ff) )

## July 29, 2024

Feature

You can now apply range and inequality filters to multiple fields in a query. This feature is generally available (GA).

For more information, see [Query with range and inequality filters on multiple fields overview](/datastore/docs/multiple-range-fields) .

## July 01, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [9.1.0](https://github.com/googleapis/nodejs-datastore/compare/v9.0.0...v9.1.0) (2024-06-24)

##### Features

  - New transaction feature ( [\#1239](https://github.com/googleapis/nodejs-datastore/issues/1239) ) ( [cdd2ee9](https://github.com/googleapis/nodejs-datastore/commit/cdd2ee98c50b48b9a2a8cfb2f66b84a5937b3783) )

##### Bug Fixes

  - **deps:** Update dependency sinon to v18 ( [\#1250](https://github.com/googleapis/nodejs-datastore/issues/1250) ) ( [b7ff5c8](https://github.com/googleapis/nodejs-datastore/commit/b7ff5c86306f80d93f678a0638892c58a3b2088c) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.20.2](https://github.com/googleapis/java-datastore/compare/v2.20.1...v2.20.2) (2024-06-28)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.32.0 ( [\#1492](https://github.com/googleapis/java-datastore/issues/1492) ) ( [d940c93](https://github.com/googleapis/java-datastore/commit/d940c937959942d753f9215e7ce940ab6742be46) )

## June 28, 2024

Feature

[Scheduled backups](/firestore/docs/backups) are now available in GA.

## June 17, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Go

### Changes for [datastore/admin/apiv1](https://github.com/googleapis/google-cloud-go/tree/main/datastore/admin/apiv1)

#### [1.17.1](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.17.0...datastore/v1.17.1) (2024-06-10)

##### Bug Fixes

  - **datastore:** Regenerate protos in new namespace ( [\#10158](https://github.com/googleapis/google-cloud-go/issues/10158) ) ( [8875511](https://github.com/googleapis/google-cloud-go/commit/8875511ca0c640d1260248f51c7b88e55136cdc6) ), refs [\#10155](https://github.com/googleapis/google-cloud-go/issues/10155)
  - **datastore:** Update retry transaction logic to be inline with Spanner ( [\#10349](https://github.com/googleapis/google-cloud-go/issues/10349) ) ( [5929a6e](https://github.com/googleapis/google-cloud-go/commit/5929a6e67891b425d33128155af5cc76ecfc87a1) )

## June 10, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.20.1](https://github.com/googleapis/java-datastore/compare/v2.20.0...v2.20.1) (2024-06-04)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.31.0 ( [\#1471](https://github.com/googleapis/java-datastore/issues/1471) ) ( [42c643d](https://github.com/googleapis/java-datastore/commit/42c643d78562c5cbd6c17c29a0a124be8d05198a) )
  - Update dependency com.google.errorprone:error\_prone\_core to v2.28.0 ( [\#1469](https://github.com/googleapis/java-datastore/issues/1469) ) ( [e3fac2b](https://github.com/googleapis/java-datastore/commit/e3fac2bf9992fcb2e91319df0520094865de2d49) )
  - Update dependency com.google.guava:guava-testlib to v33.2.1-jre ( [\#1470](https://github.com/googleapis/java-datastore/issues/1470) ) ( [614e930](https://github.com/googleapis/java-datastore/commit/614e930f2bdccc517d4733e5fb7f3cefad696a20) )

## June 03, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [9.0.0](https://github.com/googleapis/nodejs-datastore/compare/v8.7.0...v9.0.0) (2024-05-09)

##### ⚠ BREAKING CHANGES

  - An existing method `  UpdateVehicleLocation  ` is removed from service `  VehicleService  ` ( [\#1248](https://github.com/googleapis/nodejs-datastore/issues/1248) )

##### Features

  - Query profiling feature ( [\#1221](https://github.com/googleapis/nodejs-datastore/issues/1221) ) ( [414dec4](https://github.com/googleapis/nodejs-datastore/commit/414dec4e1548f551be06df914d6b56362bdc1790) )

##### Bug Fixes

  - An existing method `  UpdateVehicleLocation  ` is removed from service `  VehicleService  ` ( [\#1248](https://github.com/googleapis/nodejs-datastore/issues/1248) ) ( [ba79118](https://github.com/googleapis/nodejs-datastore/commit/ba79118ac00ccc3bb0380ee5693c3b687a7ae9c7) )
  - Read time should be used for transaction reads ( [\#1171](https://github.com/googleapis/nodejs-datastore/issues/1171) ) ( [73a0a39](https://github.com/googleapis/nodejs-datastore/commit/73a0a39b4c0423a5b4802076cdce80fce7c9adda) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.20.0](https://github.com/googleapis/java-datastore/compare/v2.19.3...v2.20.0) (2024-05-27)

##### Features

  - New PropertyMask field which allows partial commits, lookups, and query results ( [\#1455](https://github.com/googleapis/java-datastore/issues/1455) ) ( [ff5e397](https://github.com/googleapis/java-datastore/commit/ff5e39775446216b4806f55f14dacb7fc8e8854b) )

##### Bug Fixes

  - Migrate off TextPrinter's deprecated methods ( [\#1452](https://github.com/googleapis/java-datastore/issues/1452) ) ( [c3c1317](https://github.com/googleapis/java-datastore/commit/c3c131735863d71971110e2ac7ac0244ce16ee92) )
  - Set the correct database id on the key parent when calling Key\#getParent ( [\#1457](https://github.com/googleapis/java-datastore/issues/1457) ) ( [992815d](https://github.com/googleapis/java-datastore/commit/992815d9989d04f7b371dfa320ed17894626a07f) )

## May 20, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.19.3](https://github.com/googleapis/java-datastore/compare/v2.19.2...v2.19.3) (2024-05-16)

##### Dependencies

  - Update actions/checkout action to v4 ( [\#1390](https://github.com/googleapis/java-datastore/issues/1390) ) ( [80dbca1](https://github.com/googleapis/java-datastore/commit/80dbca1246facf21b08d33e5c6a09b9708b6ce63) )
  - Update dependency com.google.cloud:sdk-platform-java-config to v3.30.1 ( [\#1443](https://github.com/googleapis/java-datastore/issues/1443) ) ( [79f6c46](https://github.com/googleapis/java-datastore/commit/79f6c46bdbabc66082f23e9562ee9541e0fdeac9) )

## May 13, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Go

### Changes for [datastore/admin/apiv1](https://github.com/googleapis/google-cloud-go/tree/main/datastore/admin/apiv1)

#### [1.17.0](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.16.0...datastore/v1.17.0) (2024-05-08)

##### Features

  - **datastore:** Add query profiling ( [\#9200](https://github.com/googleapis/google-cloud-go/issues/9200) ) ( [b0235bb](https://github.com/googleapis/google-cloud-go/commit/b0235bb3828cea64b87cac3d1d84e42f1b2744ab) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.19.2](https://github.com/googleapis/java-datastore/compare/v2.19.1...v2.19.2) (2024-05-03)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.39.0 ( [\#1406](https://github.com/googleapis/java-datastore/issues/1406) ) ( [b265fb3](https://github.com/googleapis/java-datastore/commit/b265fb3c3b8ebc972edbe5a7beae816379846dac) )

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.30.0 ( [\#1426](https://github.com/googleapis/java-datastore/issues/1426) ) ( [ac3a1c1](https://github.com/googleapis/java-datastore/commit/ac3a1c10f64c8338346f8fb39f4857f47e8fc639) )
  - Update dependency com.google.errorprone:error\_prone\_core to v2.27.0 ( [\#1411](https://github.com/googleapis/java-datastore/issues/1411) ) ( [a3f5a2c](https://github.com/googleapis/java-datastore/commit/a3f5a2c24bff408479541e08278e888cf3166727) )
  - Update dependency com.google.errorprone:error\_prone\_core to v2.27.1 ( [\#1421](https://github.com/googleapis/java-datastore/issues/1421) ) ( [48d7daf](https://github.com/googleapis/java-datastore/commit/48d7dafc0c7a49e95bf41d29865ac872b0de0faf) )
  - Update dependency com.google.guava:guava-testlib to v33.2.0-jre ( [\#1422](https://github.com/googleapis/java-datastore/issues/1422) ) ( [5a5dfdf](https://github.com/googleapis/java-datastore/commit/5a5dfdfb0855cf485b875ab071b79979d24f98dd) )

## May 06, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Go

### Changes for [datastore/admin/apiv1](https://github.com/googleapis/google-cloud-go/tree/main/datastore/admin/apiv1)

#### [1.16.0](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.15.0...datastore/v1.16.0) (2024-04-29)

##### Features

  - **datastore:** Adding BeginLater and transaction state ( [\#8984](https://github.com/googleapis/google-cloud-go/issues/8984) ) ( [5f8e21f](https://github.com/googleapis/google-cloud-go/commit/5f8e21f84f0febd54e7ee6092ae6b88b269b0fc8) )
  - **datastore:** Adding BeginLater transaction option ( [\#8972](https://github.com/googleapis/google-cloud-go/issues/8972) ) ( [4067f4e](https://github.com/googleapis/google-cloud-go/commit/4067f4eabbba9e5e3265754339709fb273b73e4c) )
  - **datastore:** Adding reserve IDs support ( [\#9027](https://github.com/googleapis/google-cloud-go/issues/9027) ) ( [2d66de0](https://github.com/googleapis/google-cloud-go/commit/2d66de0c3004ca09d643c373d40e9e0f9e0f1aa5) )
  - **datastore:** Configure both mTLS and TLS endpoints for Datastore client ( [\#9653](https://github.com/googleapis/google-cloud-go/issues/9653) ) ( [38bd793](https://github.com/googleapis/google-cloud-go/commit/38bd7933f450a87886331429632fcb498a045675) )
  - **datastore:** Respect DATASTORE\_EMULATOR\_HOST setting ( [\#9789](https://github.com/googleapis/google-cloud-go/issues/9789) ) ( [7259373](https://github.com/googleapis/google-cloud-go/commit/7259373371e74cb4f7041f9397ba01dd9878b00b) )

##### Bug Fixes

  - **datastore:** Add explicit sleep before read time use ( [\#9080](https://github.com/googleapis/google-cloud-go/issues/9080) ) ( [0538be4](https://github.com/googleapis/google-cloud-go/commit/0538be457518f7b86ffcabcbad35496f053f38cc) )
  - **datastore:** Adding tracing to run method ( [\#9602](https://github.com/googleapis/google-cloud-go/issues/9602) ) ( [a5e197c](https://github.com/googleapis/google-cloud-go/commit/a5e197c78cb112836768f012c7ee4535dec8b9f5) )
  - **datastore:** Bump x/net to v0.24.0 ( [ba31ed5](https://github.com/googleapis/google-cloud-go/commit/ba31ed5fda2c9664f2e1cf972469295e63deb5b4) )
  - **datastore:** Enable universe domain resolution options ( [fd1d569](https://github.com/googleapis/google-cloud-go/commit/fd1d56930fa8a747be35a224611f4797b8aeb698) )
  - **datastore:** Prevent panic on GetMulti failure ( [\#9656](https://github.com/googleapis/google-cloud-go/issues/9656) ) ( [55845ad](https://github.com/googleapis/google-cloud-go/commit/55845ad9215191f1889b10d10fa72c9a42815d41) )
  - **datastore:** Update protobuf dep to v1.33.0 ( [30b038d](https://github.com/googleapis/google-cloud-go/commit/30b038d8cac0b8cd5dd4761c87f3f298760dd33a) )

## April 29, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.19.1](https://github.com/googleapis/java-datastore/compare/v2.19.0...v2.19.1) (2024-04-19)

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.29.0 ( [\#1403](https://github.com/googleapis/java-datastore/issues/1403) ) ( [d23dc4c](https://github.com/googleapis/java-datastore/commit/d23dc4c26a95f2c323ade4db9a88d5435a173be8) )

Feature

Firestore in Datastore mode now supports the `  us-south1  ` Dallas region.

For a full list of supported locations, see [Locations](/datastore/docs/locations) .

## April 08, 2024

Feature

Firestore in Datastore mode now supports the following additional locations:

  - `  africa-south1  ` Johannesburg
  - `  europe-north1  ` Finland
  - `  europe-southwest1  ` Madrid
  - `  europe-west10  ` Berlin
  - `  europe-west12  ` Turin
  - `  europe-west8  ` Milan
  - `  southamerica-west1  ` Santiago
  - `  us-central1  ` Iowa
  - `  us-east5  ` Columbus

For a full list of supported locations, see [Locations](/datastore/docs/locations) .

## April 05, 2024

Feature

Support for [Customer-managed encryption keys (CMEK)](/datastore/docs/cmek) . This feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

## April 01, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [8.6.0](https://github.com/googleapis/nodejs-datastore/compare/v8.5.0...v8.6.0) (2024-03-25)

##### Features

  - Add new types ExplainOptions, ExplainMetrics, PlanSummary, ExecutionStats ( [\#1241](https://github.com/googleapis/nodejs-datastore/issues/1241) ) ( [6c409d5](https://github.com/googleapis/nodejs-datastore/commit/6c409d5c922288bd8286917b266cdb553cfd43cf) )
  - Nodejs transaction redesign feature branch ( [\#1235](https://github.com/googleapis/nodejs-datastore/issues/1235) ) ( [1585d4a](https://github.com/googleapis/nodejs-datastore/commit/1585d4a4e1b4b16d198307a3e97ffcf156d000b1) )

##### Bug Fixes

  - **deps:** Update dependency async-mutex to ^0.5.0 ( [\#1240](https://github.com/googleapis/nodejs-datastore/issues/1240) ) ( [0ba1281](https://github.com/googleapis/nodejs-datastore/commit/0ba1281efe16ef0b725937627445c32c36b9f705) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.19.0](https://github.com/googleapis/java-datastore/compare/v2.18.6...v2.19.0) (2024-03-25)

##### Features

  - Implement query profile ( [\#1365](https://github.com/googleapis/java-datastore/issues/1365) ) ( [2515ed6](https://github.com/googleapis/java-datastore/commit/2515ed6cf733df84069309a3055a21cdd65c9c90) )

## March 27, 2024

Feature

Support for [Query Explain](/datastore/docs/query-explain-analyze) . This feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

Query Explain lets you submit queries and receive detailed query plan, billing and performance statistics on query execution in return. It helps you understand how your queries are executed, showing you inefficiencies.

It functions like the `  EXPLAIN [ANALYZE]  ` operation in many relational database systems.

For more information, see the [guide for Query Explain](/datastore/docs/query-explain-analyze) .

Feature

Datastore now supports using [range and inequality filters on multiple fields](/datastore/docs/multiple-range-fields) in a single query. This feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

## March 25, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-ndb](https://github.com/googleapis/python-ndb)

#### [2.3.1](https://github.com/googleapis/python-ndb/compare/v2.3.0...v2.3.1) (2024-03-16)

##### Bug Fixes

  - **grpc:** Fix large payload handling when using the emulator. ( [\#975](https://github.com/googleapis/python-ndb/issues/975) ) ( [d9162ae](https://github.com/googleapis/python-ndb/commit/d9162aee709062683bf5f9f01208bd40f46d490a) )
  - Remove uses of six. [\#913](https://github.com/googleapis/python-ndb/issues/913) ( [\#958](https://github.com/googleapis/python-ndb/issues/958) ) ( [e17129a](https://github.com/googleapis/python-ndb/commit/e17129a2114c3f5d45b99cc9a4911b586eb3fafa) )
  - Show a non-None error for core\_exception.Unknown errors. ( [\#968](https://github.com/googleapis/python-ndb/issues/968) ) ( [66e61cc](https://github.com/googleapis/python-ndb/commit/66e61cc578335509d480650906528fa390f44c11) )

##### Documentation

  - Document how to run system tests against the emulator. ( [\#963](https://github.com/googleapis/python-ndb/issues/963) ) ( [47db5b9](https://github.com/googleapis/python-ndb/commit/47db5b9f6ee1fc7c01ad86d476cd8e066fb5cffb) )
  - Note to use functools.wrap instead of utils.wrapping. ( [\#966](https://github.com/googleapis/python-ndb/issues/966) ) ( [5e9f3d6](https://github.com/googleapis/python-ndb/commit/5e9f3d6977677c20b3447f07bf8bcf4553aac076) )
  - Tell users of utils.wrapping to use functools.wraps ( [\#967](https://github.com/googleapis/python-ndb/issues/967) ) ( [042645b](https://github.com/googleapis/python-ndb/commit/042645b52608a1c11645dd4b014a90040468b113) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.18.6](https://github.com/googleapis/java-datastore/compare/v2.18.5...v2.18.6) (2024-03-18)

##### Bug Fixes

  - **deps:** Update the Java code generator (gapic-generator-java) to 2.37.0 ( [\#1355](https://github.com/googleapis/java-datastore/issues/1355) ) ( [bcc5668](https://github.com/googleapis/java-datastore/commit/bcc5668039d4dd2055e9666a65fcda3984fc33b5) )

##### Dependencies

  - Update dependency com.google.cloud:sdk-platform-java-config to v3.28.0 ( [\#1372](https://github.com/googleapis/java-datastore/issues/1372) ) ( [09db2a7](https://github.com/googleapis/java-datastore/commit/09db2a75fa714a909bc6fa9b43a9213ae6467c84) )
  - Update dependency com.google.cloud:sdk-platform-java-config to v3.28.1 ( [\#1373](https://github.com/googleapis/java-datastore/issues/1373) ) ( [c6e63e5](https://github.com/googleapis/java-datastore/commit/c6e63e5f876fdda953935d09f0536a90a98a812c) )
  - Update dependency com.google.errorprone:error\_prone\_core to v2.26.0 ( [\#1361](https://github.com/googleapis/java-datastore/issues/1361) ) ( [9442766](https://github.com/googleapis/java-datastore/commit/9442766ad61b0c1001d36ecfc0668308838b4a83) )
  - Update dependency com.google.errorprone:error\_prone\_core to v2.26.1 ( [\#1363](https://github.com/googleapis/java-datastore/issues/1363) ) ( [05fe5bc](https://github.com/googleapis/java-datastore/commit/05fe5bccf97dae92c00f2eead98424771cb321fd) )
  - Update dependency com.google.guava:guava-testlib to v33.1.0-jre ( [\#1368](https://github.com/googleapis/java-datastore/issues/1368) ) ( [0195345](https://github.com/googleapis/java-datastore/commit/0195345630f404bbcaf1601ded8a8e2011fc3e6e) )

## March 05, 2024

Feature

You can now use the Firestore emulator to test Firestore in Datastore mode behavior. Use [`  gcloud emulators firestore start  ` with `  --database-mode=datastore-mode  `](/datastore/docs/emulator) .

## March 04, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-ndb](https://github.com/googleapis/python-ndb)

#### [2.3.0](https://github.com/googleapis/python-ndb/compare/v2.2.2...v2.3.0) (2024-03-01)

##### Features

  - Add field information when raising validation errors. ( [\#956](https://github.com/googleapis/python-ndb/issues/956) ) ( [17caf0b](https://github.com/googleapis/python-ndb/commit/17caf0b5f7d0c4d18522f676c8af990b8ff8462d) )
  - Add Python 3.12 ( [\#949](https://github.com/googleapis/python-ndb/issues/949) ) ( [b5c8477](https://github.com/googleapis/python-ndb/commit/b5c847783b80071c2dd9e9a3dbf899230c99e64a) )
  - Add support for google.cloud.ndb. **version** ( [\#929](https://github.com/googleapis/python-ndb/issues/929) ) ( [42b3f01](https://github.com/googleapis/python-ndb/commit/42b3f0137caed25ac3242435b571155d2d84c78e) )
  - Add support for server side NOT\_IN filter. ( [\#957](https://github.com/googleapis/python-ndb/issues/957) ) ( [f0b0724](https://github.com/googleapis/python-ndb/commit/f0b0724d7e364cc3f3574e77076465657089b09c) )
  - Allow queries using server side IN. ( [\#954](https://github.com/googleapis/python-ndb/issues/954) ) ( [2646cef](https://github.com/googleapis/python-ndb/commit/2646cef3e2687461174a11c45f29de7b84d1fcdb) )
  - Introduce compatibility with native namespace packages ( [\#933](https://github.com/googleapis/python-ndb/issues/933) ) ( [ccae387](https://github.com/googleapis/python-ndb/commit/ccae387720a28db2686e69dfe23a2599fc4908f0) )
  - Use server side \!= for queries. ( [\#950](https://github.com/googleapis/python-ndb/issues/950) ) ( [106772f](https://github.com/googleapis/python-ndb/commit/106772f031f6c37500a0d463698e59008f9bf19a) )

##### Bug Fixes

  - Compressed repeated to uncompressed property ( [\#772](https://github.com/googleapis/python-ndb/issues/772) ) ( [dab9edf](https://github.com/googleapis/python-ndb/commit/dab9edf0fc161051eb13c296cbe973b3a16b502d) )
  - Repeated structured property containing blob property with legacy\_data ( [\#817](https://github.com/googleapis/python-ndb/issues/817) ) ( [\#946](https://github.com/googleapis/python-ndb/issues/946) ) ( [455f860](https://github.com/googleapis/python-ndb/commit/455f860343ff1b71232dad98cf91415492a899ca) )

##### Documentation

  - ****init** :** Note that Firestore in Datastore Mode is supported ( [\#919](https://github.com/googleapis/python-ndb/issues/919) ) ( [0fa75e7](https://github.com/googleapis/python-ndb/commit/0fa75e71dfc6d56d2c0eaf214a48774b99bb959f) )
  - Correct read\_consistency docs. ( [\#948](https://github.com/googleapis/python-ndb/issues/948) ) ( [7e8481d](https://github.com/googleapis/python-ndb/commit/7e8481db84a6d0b96cf09c38e90f47d6b7847a0b) )
  - Fix a mistaken ID description ( [\#943](https://github.com/googleapis/python-ndb/issues/943) ) ( [5103813](https://github.com/googleapis/python-ndb/commit/51038139e45807b3a14346ded702fbe202dcfdf2) )
  - Show how to use named databases ( [\#932](https://github.com/googleapis/python-ndb/issues/932) ) ( [182fe4e](https://github.com/googleapis/python-ndb/commit/182fe4e2d295768aaf016f94cb43b6b1e5572ebd) )

## January 29, 2024

Feature

[Eventarc events](/datastore/docs/eventarc) and [Firestore events for Cloud Functions (2nd gen)](/datastore/docs/extend-with-functions-2nd-gen) are now supported at the General Availability ( [GA](https://cloud.google.com/products#product-launch-stages) ) level.

## January 15, 2024

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.18.0](https://github.com/googleapis/java-datastore/compare/v2.17.6...v2.18.0) (2024-01-08)

##### Features

  - Remove `  @BetaApi  ` annotations from get/setDatabaseId methods ( [\#1272](https://github.com/googleapis/java-datastore/issues/1272) ) ( [2bd9a51](https://github.com/googleapis/java-datastore/commit/2bd9a51122248ee242bbcd4914e219d9d5e435bb) )

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.21.0 ( [\#1280](https://github.com/googleapis/java-datastore/issues/1280) ) ( [ac253dc](https://github.com/googleapis/java-datastore/commit/ac253dca1add844124ca03039a996196e09a1759) )
  - Update dependency com.google.errorprone:error\_prone\_core to v2.24.1 ( [\#1274](https://github.com/googleapis/java-datastore/issues/1274) ) ( [86cd785](https://github.com/googleapis/java-datastore/commit/86cd7856463c5039601afc10fecc1b28727d4906) )

## January 10, 2024

Feature

The ability to [create multiple databases per project](/datastore/docs/manage-databases) is now supported at the [General Availability level](https://cloud.google.com/products/#product-launch-stages) .

## January 02, 2024

Feature

Support for the [europe-west1 (Belgium) and me-central2 (Dammam) locations](/datastore/docs/locations) .

## December 20, 2023

Feature

[Index scans in Key Visualizer](/datastore/docs/keyvis-patterns-index) are now supported at the General Availability ( [GA](https://cloud.google.com/products#product-launch-stages) ) level.

## December 18, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [8.3.0](https://github.com/googleapis/nodejs-datastore/compare/v8.2.2...v8.3.0) (2023-12-11)

##### Features

  - Allow the user to set fallback to rest ( [\#1203](https://github.com/googleapis/nodejs-datastore/issues/1203) ) ( [8a1fa54](https://github.com/googleapis/nodejs-datastore/commit/8a1fa54e3873230256895c48b8b9c6889f75dd98) )

##### Bug Fixes

  - Change tests to use new filter and use gax warn for warning just once ( [\#1185](https://github.com/googleapis/nodejs-datastore/issues/1185) ) ( [532711b](https://github.com/googleapis/nodejs-datastore/commit/532711bfd19b1a12844b02fd314f1703be4b0125) )
  - **deps:** Update dependency sinon to v17 ( [\#1183](https://github.com/googleapis/nodejs-datastore/issues/1183) ) ( [52adb5e](https://github.com/googleapis/nodejs-datastore/commit/52adb5e13ddc123c2bed33df76be76760d33c06e) )

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.19.0](https://github.com/googleapis/python-datastore/compare/v2.18.0...v2.19.0) (2023-12-10)

##### Features

  - Add support for Python 3.12 ( [\#498](https://github.com/googleapis/python-datastore/issues/498) ) ( [d1d60fa](https://github.com/googleapis/python-datastore/commit/d1d60fa602eca2062a505a0750b0ce6dccc771cd) )
  - Introduce compatibility with native namespace packages ( [\#497](https://github.com/googleapis/python-datastore/issues/497) ) ( [87b3392](https://github.com/googleapis/python-datastore/commit/87b339228896da197b0ee77e2b00994431ae8d2e) )

##### Bug Fixes

  - Use `  retry_async  ` instead of `  retry  ` in async client ( [4e15ce6](https://github.com/googleapis/python-datastore/commit/4e15ce640580f14fb1ee5d8ad49ea48e860ff1da) )

##### Documentation

  - Minor formatting ( [\#476](https://github.com/googleapis/python-datastore/issues/476) ) ( [b13b15c](https://github.com/googleapis/python-datastore/commit/b13b15cd95c02c923f9991b088bb71eda777cf46) )

## December 15, 2023

Feature

You can now [create and delete non-default databases](/datastore/docs/manage-databases#create_a_database) in the Google Cloud console.

## December 04, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.17.6](https://github.com/googleapis/java-datastore/compare/v2.17.5...v2.17.6) (2023-11-30)

##### Bug Fixes

  - Remove deprecated `  databaseId  ` field in DatastoreOptions ( [\#1237](https://github.com/googleapis/java-datastore/issues/1237) ) ( [05e25e5](https://github.com/googleapis/java-datastore/commit/05e25e5d31f72f9cdedbb5efa85c64b55ccbc405) )

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.20.0 ( [\#1247](https://github.com/googleapis/java-datastore/issues/1247) ) ( [c4e3533](https://github.com/googleapis/java-datastore/commit/c4e3533fe357827cc25d0f029e5a83ced31db12a) )
  - Update dependency org.junit.vintage:junit-vintage-engine to v5.10.1 ( [\#1230](https://github.com/googleapis/java-datastore/issues/1230) ) ( [05c7fc6](https://github.com/googleapis/java-datastore/commit/05c7fc69d52f5a9026a6529f638fe6164860e8f9) )

## November 10, 2023

Feature

Support for Firestore in Datastore mode [point-in-time recovery (PITR)](/datastore/docs/pitr) feature that provides protection against accidental deletion or writes is now [generally available (GA)](https://cloud.google.com/products#product-launch-stages) .

## November 06, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.17.5](https://github.com/googleapis/java-datastore/compare/v2.17.4...v2.17.5) (2023-11-02)

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.19.0 ( [\#1226](https://github.com/googleapis/java-datastore/issues/1226) ) ( [970ac96](https://github.com/googleapis/java-datastore/commit/970ac9652ad16848ccfb26ce248e66956693be9e) )

## October 30, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.17.4](https://github.com/googleapis/java-datastore/compare/v2.17.3...v2.17.4) (2023-10-23)

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.18.0 ( [\#1215](https://github.com/googleapis/java-datastore/issues/1215) ) ( [aa82f01](https://github.com/googleapis/java-datastore/commit/aa82f019bcf90f99e6d3d2c96a52d8f2b9a8d27a) )
  - Update dependency com.google.errorprone:error\_prone\_core to v2.23.0 ( [\#1213](https://github.com/googleapis/java-datastore/issues/1213) ) ( [c57db43](https://github.com/googleapis/java-datastore/commit/c57db43c783ba6ec16a55d470664990e932971ef) )
  - Update dependency org.graalvm.buildtools:junit-platform-native to v0.9.28 ( [\#1216](https://github.com/googleapis/java-datastore/issues/1216) ) ( [ce4eff2](https://github.com/googleapis/java-datastore/commit/ce4eff24aae8d1e6e02558e627c033dc138891e6) )
  - Update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.28 ( [\#1217](https://github.com/googleapis/java-datastore/issues/1217) ) ( [7d56b3c](https://github.com/googleapis/java-datastore/commit/7d56b3cee53e0852873896f7fd22a0414d4b7d83) )

## October 16, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.17.3](https://github.com/googleapis/java-datastore/compare/v2.17.2...v2.17.3) (2023-10-10)

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.17.0 ( [\#1206](https://github.com/googleapis/java-datastore/issues/1206) ) ( [2ad068b](https://github.com/googleapis/java-datastore/commit/2ad068b115c6ff7c59394fdba5e0e445028a3fee) )

## October 09, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [8.2.1](https://github.com/googleapis/nodejs-datastore/compare/v8.2.0...v8.2.1) (2023-10-03)

##### Bug Fixes

  - Make aggregation query requests run properly inside a transaction ( [\#1166](https://github.com/googleapis/nodejs-datastore/issues/1166) ) ( [263804b](https://github.com/googleapis/nodejs-datastore/commit/263804b768322de39bf87b4c5265c303a2bda173) )

#### [8.2.0](https://github.com/googleapis/nodejs-datastore/compare/v8.1.0...v8.2.0) (2023-10-02)

##### Features

  - Support for using multiple databases in datastore ( [\#1090](https://github.com/googleapis/nodejs-datastore/issues/1090) ) ( [10ce563](https://github.com/googleapis/nodejs-datastore/commit/10ce563dae7e1164d3ee23a5887265c9de7b106f) )

##### Bug Fixes

  - Allow users to set environment variable to connect to emulator running on docker ( [\#1164](https://github.com/googleapis/nodejs-datastore/issues/1164) ) ( [a41741b](https://github.com/googleapis/nodejs-datastore/commit/a41741b1412b1854aeecbe50441aa85015c3d399) )
  - Check property existence for exclude from indexes with wildcard ( [\#1114](https://github.com/googleapis/nodejs-datastore/issues/1114) ) ( [e6b8ef7](https://github.com/googleapis/nodejs-datastore/commit/e6b8ef74ff10107943d0ae194f9a8d540d8557c1) )
  - **deps:** Update dependency sinon to v16 ( [\#1150](https://github.com/googleapis/nodejs-datastore/issues/1150) ) ( [0d8b715](https://github.com/googleapis/nodejs-datastore/commit/0d8b7153fc156a4b55e965f39161bd5c19bffff6) )

### Go

### Changes for [datastore/admin/apiv1](https://github.com/googleapis/google-cloud-go/tree/main/datastore/admin/apiv1)

#### [1.15.0](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.14.0...datastore/v1.15.0) (2023-10-06)

##### Features

  - **datastore:** Adding dynamic routing header ( [\#8364](https://github.com/googleapis/google-cloud-go/issues/8364) ) ( [d235a42](https://github.com/googleapis/google-cloud-go/commit/d235a427a4e8d84466599cad4a68539a7a57a5db) )

##### Bug Fixes

  - **datastore:** Allow saving nested byte slice ( [\#8540](https://github.com/googleapis/google-cloud-go/issues/8540) ) ( [8e53787](https://github.com/googleapis/google-cloud-go/commit/8e53787eac6f724ea4282533349abef3cbaffefe) )
  - **datastore:** Handle loading nil values ( [\#8544](https://github.com/googleapis/google-cloud-go/issues/8544) ) ( [25dbb9c](https://github.com/googleapis/google-cloud-go/commit/25dbb9cf1041d9e19edecd5c48b698b6f81f2d20) )

## October 02, 2023

Change

Raised the maximum number of composite indexes from 200 to 500 for projects with billing enabled. The limit is 200 for projects without billing enabled.

For more information about limits, see [Limits](/datastore/docs/concepts/limits) .

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-ndb](https://github.com/googleapis/python-ndb)

#### [2.2.2](https://github.com/googleapis/python-ndb/compare/v2.2.1...v2.2.2) (2023-09-19)

##### Documentation

  - **query:** Document deprecation of Query.default\_options ( [\#915](https://github.com/googleapis/python-ndb/issues/915) ) ( [a656719](https://github.com/googleapis/python-ndb/commit/a656719d8a4f20a8b8dc564a1e3837a2cfb037c4) ), closes [\#880](https://github.com/googleapis/python-ndb/issues/880)

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.17.2](https://github.com/googleapis/java-datastore/compare/v2.17.1...v2.17.2) (2023-09-26)

##### Bug Fixes

  - Checksum format ( [\#1178](https://github.com/googleapis/java-datastore/issues/1178) ) ( [410b939](https://github.com/googleapis/java-datastore/commit/410b9397bb9ba480dff6217c0c4c27364e58db49) )
  - Deprecate `  databaseId  ` on datastore-v1-proto-client DatastoreOptions ( [\#1190](https://github.com/googleapis/java-datastore/issues/1190) ) ( [12a3d27](https://github.com/googleapis/java-datastore/commit/12a3d27ebc7ca87338ee896fd6ba3e804edd95ce) )

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.16.0 ( [\#1195](https://github.com/googleapis/java-datastore/issues/1195) ) ( [6f0cad7](https://github.com/googleapis/java-datastore/commit/6f0cad7268cee6347d34125c14c1133b80c840d7) )
  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.16.1 ( [\#1198](https://github.com/googleapis/java-datastore/issues/1198) ) ( [8062be9](https://github.com/googleapis/java-datastore/commit/8062be94b00fe2967e592f3d0a35751f0d11a013) )
  - Update dependency com.google.errorprone:error\_prone\_core to v2.22.0 ( [\#1194](https://github.com/googleapis/java-datastore/issues/1194) ) ( [b8f108a](https://github.com/googleapis/java-datastore/commit/b8f108a3d013b5b54c519db24b40dd63e4855240) )
  - Update dependency org.graalvm.buildtools:junit-platform-native to v0.9.26 ( [\#1176](https://github.com/googleapis/java-datastore/issues/1176) ) ( [76e3a71](https://github.com/googleapis/java-datastore/commit/76e3a71560222894513a485cb91cec7161276e3c) )
  - Update dependency org.graalvm.buildtools:junit-platform-native to v0.9.27 ( [\#1192](https://github.com/googleapis/java-datastore/issues/1192) ) ( [aa3bca1](https://github.com/googleapis/java-datastore/commit/aa3bca10de19350cabc244426ebc284c64cb7344) )
  - Update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.26 ( [\#1177](https://github.com/googleapis/java-datastore/issues/1177) ) ( [7733004](https://github.com/googleapis/java-datastore/commit/7733004aff34bb8b4b8addccc68e75080f0f33a5) )
  - Update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.27 ( [\#1193](https://github.com/googleapis/java-datastore/issues/1193) ) ( [a628255](https://github.com/googleapis/java-datastore/commit/a628255dffc2e8f871df699ebe7a94e4b75eb4b9) )
  - Update gapic-generator-java to 2.26.0 ( [\#1197](https://github.com/googleapis/java-datastore/issues/1197) ) ( [2540282](https://github.com/googleapis/java-datastore/commit/2540282653d8f8f06a71568c81eca8d3cb70f00f) )

## September 25, 2023

Feature

Support for [europe-west9 (Paris), me-central1 (Doha), and me-west1 (Tel Aviv)](/datastore/docs/locations) .

## September 18, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [8.1.0](https://github.com/googleapis/nodejs-datastore/compare/v8.0.0...v8.1.0) (2023-09-07)

##### Features

  - Sum and average aggregation queries ( [\#1097](https://github.com/googleapis/nodejs-datastore/issues/1097) ) ( [44ba6f8](https://github.com/googleapis/nodejs-datastore/commit/44ba6f8f84ef3e33aa1c07b0808a42bcf871b8c6) )

##### Bug Fixes

  - Simplify logic for HTTP/1.1 REST fallback option ( [\#1138](https://github.com/googleapis/nodejs-datastore/issues/1138) ) ( [4cefaea](https://github.com/googleapis/nodejs-datastore/commit/4cefaeab2ee8af800303f09495883aa1a5a28632) )

### Python

### Changes for [google-cloud-ndb](https://github.com/googleapis/python-ndb)

#### [2.2.1](https://github.com/googleapis/python-ndb/compare/v2.2.0...v2.2.1) (2023-09-15)

##### Bug Fixes

  - **deps:** Add missing six dependency ( [\#912](https://github.com/googleapis/python-ndb/issues/912) ) ( [3b1ffb7](https://github.com/googleapis/python-ndb/commit/3b1ffb7e5cabdadfe2a4be6802adef774eec5ef8) )

##### Documentation

  - Mark database argument for get\_by\_id and its async counterpart as ignored ( [\#905](https://github.com/googleapis/python-ndb/issues/905) ) ( [b0f4310](https://github.com/googleapis/python-ndb/commit/b0f431048b7b2ebb20e4255340290c7687e27425) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.17.1](https://github.com/googleapis/java-datastore/compare/v2.17.0...v2.17.1) (2023-09-11)

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.15.0 ( [\#1184](https://github.com/googleapis/java-datastore/issues/1184) ) ( [6cbb795](https://github.com/googleapis/java-datastore/commit/6cbb79589e7eb8648c734bd02579a93423aa4e13) )
  - Update dependency org.easymock:easymock to v5.2.0 ( [\#1180](https://github.com/googleapis/java-datastore/issues/1180) ) ( [3e62380](https://github.com/googleapis/java-datastore/commit/3e62380ae2793437aa9c4d21fa4484a8896cb49e) )

##### Documentation

  - Marking AggregationResult\#get as Obsolete ( [\#1185](https://github.com/googleapis/java-datastore/issues/1185) ) ( [252f854](https://github.com/googleapis/java-datastore/commit/252f8549895250ced3aecf5c082cb0b41ea12472) )

## September 11, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.18.0](https://github.com/googleapis/python-datastore/compare/v2.17.0...v2.18.0) (2023-09-05)

##### Features

  - Add support for Sum and Avg aggregation query ( [\#437](https://github.com/googleapis/python-datastore/issues/437) ) ( [e99120d](https://github.com/googleapis/python-datastore/commit/e99120d0dde446d89674addab49987cb24279fe3) )

##### Documentation

  - Update property requirement specifications ( [\#470](https://github.com/googleapis/python-datastore/issues/470) ) ( [795ce81](https://github.com/googleapis/python-datastore/commit/795ce81c61d2af4e1ba285b4f0f8d796ea435bc3) )

## August 28, 2023

Feature

The [`  sum()  ` and `  avg()  ` aggregation functions](/datastore/docs/aggregation-queries) are now available for Firestore in Datastore mode.

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Go

### Changes for [datastore/admin/apiv1](https://github.com/googleapis/google-cloud-go/tree/main/datastore/admin/apiv1)

#### [1.14.0](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.13.0...datastore/v1.14.0) (2023-08-22)

##### Features

  - **datastore:** SUM and AVG aggregations ( [\#8307](https://github.com/googleapis/google-cloud-go/issues/8307) ) ( [a9fff18](https://github.com/googleapis/google-cloud-go/commit/a9fff181e4ea8281ad907e7b2e0d90e70013a4de) )
  - **datastore:** Support aggregation query in transaction ( [\#8439](https://github.com/googleapis/google-cloud-go/issues/8439) ) ( [37681ff](https://github.com/googleapis/google-cloud-go/commit/37681ff291c0ccf4c908be55b97639c04b9dec48) )

##### Bug Fixes

  - **datastore:** Correcting string representation of Key ( [\#8363](https://github.com/googleapis/google-cloud-go/issues/8363) ) ( [4cb1211](https://github.com/googleapis/google-cloud-go/commit/4cb12110ba229dfbe21568eb06c243bdffd1fee7) )
  - **datastore:** Fix NoIndex for array property ( [\#7674](https://github.com/googleapis/google-cloud-go/issues/7674) ) ( [01951e6](https://github.com/googleapis/google-cloud-go/commit/01951e64f3955dc337172a30d78e2f92f65becb2) )

##### Documentation

  - **datastore/admin:** Specify limit for `  properties  ` in `  Index  ` message in Datastore Admin API ( [b890425](https://github.com/googleapis/google-cloud-go/commit/b8904253a0f8424ea4548469e5feef321bd7396a) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.17.0](https://github.com/googleapis/java-datastore/compare/v2.16.3...v2.17.0) (2023-08-22)

##### Features

  - Publish proto definitions for SUM/AVG in Datastore ( [\#1157](https://github.com/googleapis/java-datastore/issues/1157) ) ( [954320a](https://github.com/googleapis/java-datastore/commit/954320aaefec249c77c757a1610727519a4029bd) )
  - Sum and Avg aggregation feature ( [\#1067](https://github.com/googleapis/java-datastore/issues/1067) ) ( [56d1001](https://github.com/googleapis/java-datastore/commit/56d1001005cf7d52f8ba3e5258d6401be729bdbf) )

##### Dependencies

  - Update dependency com.google.errorprone:error\_prone\_core to v2.21.1 ( [\#1163](https://github.com/googleapis/java-datastore/issues/1163) ) ( [83158b6](https://github.com/googleapis/java-datastore/commit/83158b6172a4a61b3e2a86dea6271ff7f9f84f6b) )
  - Update dependency org.graalvm.buildtools:junit-platform-native to v0.9.24 ( [\#1165](https://github.com/googleapis/java-datastore/issues/1165) ) ( [4094c70](https://github.com/googleapis/java-datastore/commit/4094c702982e4a005a36324892daee451bd16062) )
  - Update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.24 ( [\#1166](https://github.com/googleapis/java-datastore/issues/1166) ) ( [70cc371](https://github.com/googleapis/java-datastore/commit/70cc371babd674000fe6f8d78a0f42e75deb5d99) )

##### Documentation

  - Update property requirement specifications ( [\#1169](https://github.com/googleapis/java-datastore/issues/1169) ) ( [c908837](https://github.com/googleapis/java-datastore/commit/c908837ea953a5fdc87f9c83937646d309806e03) )

## August 25, 2023

Feature

[Scheduled backups](/datastore/docs/backups) now available in [Preview](https://cloud.google.com/products#product-launch-stages) .

Feature

You can now [view and list multiple databases](/datastore/docs/manage-databases#list_databases) using the Google Cloud console. This feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

## August 14, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [8.0.0](https://github.com/googleapis/nodejs-datastore/compare/v7.5.1...v8.0.0) (2023-08-09)

##### ⚠ BREAKING CHANGES

  - upgrade to Node 14

##### Miscellaneous Chores

  - Upgrade to Node 14 ( [b7904f1](https://github.com/googleapis/nodejs-datastore/commit/b7904f12b1d398a5b0e6fefc2a002c404f9e7d3d) )

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.17.0](https://github.com/googleapis/python-datastore/compare/v2.16.1...v2.17.0) (2023-08-09)

##### Documentation

  - Minor formatting in Datastore Admin API ( [cfcd0c2](https://github.com/googleapis/python-datastore/commit/cfcd0c2552c5dcf503cb3dee8c57b1e82be2d432) )
  - Specify limit for `  properties  ` in `  Index  ` message in Datastore Admin API ( [cfcd0c2](https://github.com/googleapis/python-datastore/commit/cfcd0c2552c5dcf503cb3dee8c57b1e82be2d432) )

## August 07, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.16.3](https://github.com/googleapis/java-datastore/compare/v2.16.2...v2.16.3) (2023-08-02)

##### Documentation

  - Specify limit for `  properties  ` in `  Index  ` message in Datastore Admin API ( [\#1149](https://github.com/googleapis/java-datastore/issues/1149) ) ( [00a696d](https://github.com/googleapis/java-datastore/commit/00a696d5e0fe2ffe6c9e02abd902d1b533265310) )

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.14.0 ( [\#1159](https://github.com/googleapis/java-datastore/issues/1159) ) ( [fcf07d4](https://github.com/googleapis/java-datastore/commit/fcf07d4b5b1f949f1d6b46861406cef88a9a052b) )
  - Update dependency com.google.errorprone:error\_prone\_core to v2.21.0 ( [\#1158](https://github.com/googleapis/java-datastore/issues/1158) ) ( [08dbb3a](https://github.com/googleapis/java-datastore/commit/08dbb3ab98870f74b78caa7d160271fccc134ae9) )

Feature

You can now visualize heatmap pattern for entity keys and make better workload pattern predictions. To learn more, see [Key Visualizer](/datastore/docs/key-visualizer) . This feature is in [Preview](https://cloud.google.com/products/#product-launch-stages) .

## July 31, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Go

### Changes for [datastore/admin/apiv1](https://github.com/googleapis/google-cloud-go/tree/main/datastore/admin/apiv1)

#### [1.13.0](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.12.1...datastore/v1.13.0) (2023-07-26)

##### Features

  - **datastore:** Multi DB support ( [\#8276](https://github.com/googleapis/google-cloud-go/issues/8276) ) ( [e4d07a0](https://github.com/googleapis/google-cloud-go/commit/e4d07a0dddeab7fe635840f506daf01ceb18c067) )

### Python

### Changes for [google-cloud-ndb](https://github.com/googleapis/python-ndb)

#### [2.2.0](https://github.com/googleapis/python-ndb/compare/v2.1.1...v2.2.0) (2023-07-26)

##### Features

  - Named db support ( [\#882](https://github.com/googleapis/python-ndb/issues/882) ) ( [f5713b0](https://github.com/googleapis/python-ndb/commit/f5713b0e36e54ef69e9fa7e99975f32870832f65) )

##### Documentation

  - **query:** Fix Py2-style print statements ( [\#878](https://github.com/googleapis/python-ndb/issues/878) ) ( [a3a181a](https://github.com/googleapis/python-ndb/commit/a3a181a427cc292882691d963b30bc78c05c6592) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.16.2](https://github.com/googleapis/java-datastore/compare/v2.16.1...v2.16.2) (2023-07-25)

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.13.1 ( [\#1136](https://github.com/googleapis/java-datastore/issues/1136) ) ( [f4d66af](https://github.com/googleapis/java-datastore/commit/f4d66aff3b86c656998443d12ff1eec301194cfd) )
  - Update dependency org.junit.vintage:junit-vintage-engine to v5.10.0 ( [\#1139](https://github.com/googleapis/java-datastore/issues/1139) ) ( [a170611](https://github.com/googleapis/java-datastore/commit/a170611e824d6ca6ea14c0ee57c35e3a4ab1eab0) )

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.15.1](https://github.com/googleapis/java-datastore/compare/v2.15.0...v2.15.1) (2023-07-28)

##### Dependencies

  - Shared-dependencies 3.13.0 ( [\#1146](https://github.com/googleapis/java-datastore/issues/1146) ) ( [542c628](https://github.com/googleapis/java-datastore/commit/542c6289d58f837b9b76e23f2b15d438cd54528c) )

##### Documentation

  - Fix javadoc errors ( [\#1126](https://github.com/googleapis/java-datastore/issues/1126) ) ( [\#1153](https://github.com/googleapis/java-datastore/issues/1153) ) ( [00c68b0](https://github.com/googleapis/java-datastore/commit/00c68b05da050c159a83b157cabfcee201f22c76) )

## July 17, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.16.1](https://github.com/googleapis/java-datastore/compare/v2.16.0...v2.16.1) (2023-07-10)

##### Documentation

  - Fix javadoc errors ( [\#1126](https://github.com/googleapis/java-datastore/issues/1126) ) ( [d4b11bb](https://github.com/googleapis/java-datastore/commit/d4b11bbf9198b446365b25617614434865d7e285) )

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.13.0 ( [\#1130](https://github.com/googleapis/java-datastore/issues/1130) ) ( [2181847](https://github.com/googleapis/java-datastore/commit/2181847666bce403743677b06f90b34e5ae180a3) )

## July 14, 2023

Feature

Support for Firestore in Datastore mode [point-in-time recovery (PITR)](/datastore/docs/pitr) feature that provides protection against accidental deletion or writes is now available in [Preview](https://cloud.google.com/products/#product-launch-stages) .

## July 11, 2023

Feature

Support for the [northamerica-northeast2 (Toronto)](/datastore/docs/locations) region.

## July 10, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Go

### Changes for [datastore/admin/apiv1](https://github.com/googleapis/google-cloud-go/tree/main/datastore/admin/apiv1)

#### [1.12.1](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.12.0...datastore/v1.12.1) (2023-07-07)

##### Bug Fixes

  - **datastore:** Return error from RunAggregationQuery ( [\#8222](https://github.com/googleapis/google-cloud-go/issues/8222) ) ( [a9b67cf](https://github.com/googleapis/google-cloud-go/commit/a9b67cfc95b567d29358501ec7c5883b1f90bd3e) )

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.16.1](https://github.com/googleapis/python-datastore/compare/v2.16.0...v2.16.1) (2023-07-05)

##### Bug Fixes

  - Add async context manager return types ( [\#452](https://github.com/googleapis/python-datastore/issues/452) ) ( [05f20dc](https://github.com/googleapis/python-datastore/commit/05f20dc54a100413ff7db2376ba353311584e4c8) )

## July 07, 2023

Feature

[Multiple databases](/datastore/docs/manage-databases) now available in [Preview](https://cloud.google.com/products/#product-launch-stages) .

## July 03, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Go

### Changes for [datastore/admin/apiv1](https://github.com/googleapis/google-cloud-go/tree/main/datastore/admin/apiv1)

#### [1.12.0](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.11.0...datastore/v1.12.0) (2023-06-27)

##### Features

  - **datastore:** Update all direct dependencies ( [b340d03](https://github.com/googleapis/google-cloud-go/commit/b340d030f2b52a4ce48846ce63984b28583abde6) )

##### Bug Fixes

  - **datastore:** Change aggregation result to return generic value ( [\#8167](https://github.com/googleapis/google-cloud-go/issues/8167) ) ( [9d3d17b](https://github.com/googleapis/google-cloud-go/commit/9d3d17bee90d010dab99a5a0f1610a777e55cc78) )
  - **datastore:** Handling nil slices in save and query ( [\#8043](https://github.com/googleapis/google-cloud-go/issues/8043) ) ( [36f01e9](https://github.com/googleapis/google-cloud-go/commit/36f01e99f75f4f07ae10991c52f45115b8180b45) )
  - **datastore:** PKG:datastore TYPE:datastoreClient FUNC:RunAggregationQuery ( [\#7803](https://github.com/googleapis/google-cloud-go/issues/7803) ) ( [1f050ea](https://github.com/googleapis/google-cloud-go/commit/1f050ea92782e7ec1ecb67fe134a89347a613351) )
  - **datastore:** REST query UpdateMask bug ( [df52820](https://github.com/googleapis/google-cloud-go/commit/df52820b0e7721954809a8aa8700b93c5662dc9b) )
  - **datastore:** Update grpc to v1.55.0 ( [1147ce0](https://github.com/googleapis/google-cloud-go/commit/1147ce02a990276ca4f8ab7a1ab65c14da4450ef) )

## June 27, 2023

Feature

[Eventarc events](/datastore/docs/eventarc) and [Firestore in Datastore mode events for Cloud Functions (2nd gen)](/datastore/docs/extend-with-functions-2nd-gen) now available in [Preview](https://cloud.google.com/products/#product-launch-stages) .

## June 26, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.16.0](https://github.com/googleapis/python-datastore/compare/v2.15.2...v2.16.0) (2023-06-21)

##### Features

  - Named database support ( [\#439](https://github.com/googleapis/python-datastore/issues/439) ) ( [abf0060](https://github.com/googleapis/python-datastore/commit/abf0060980b2e444f4ec66e9779900658572317e) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.16.0](https://github.com/googleapis/java-datastore/compare/v2.15.0...v2.16.0) (2023-06-22)

##### Features

  - Remove BetaApi annotation from OR query API ( [\#1118](https://github.com/googleapis/java-datastore/issues/1118) ) ( [b08dc9a](https://github.com/googleapis/java-datastore/commit/b08dc9ac796bf066e447633644c4380aa2c26753) )

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.12.0 ( [\#1121](https://github.com/googleapis/java-datastore/issues/1121) ) ( [65dd46d](https://github.com/googleapis/java-datastore/commit/65dd46d501de1360701146f4a9d7231dccd1e3c2) )
  - Update dependency com.google.errorprone:error\_prone\_core to v2.20.0 ( [\#1115](https://github.com/googleapis/java-datastore/issues/1115) ) ( [381d76e](https://github.com/googleapis/java-datastore/commit/381d76e3e079752f9f02d488603e3b89979018ea) )
  - Update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.23 ( [\#1114](https://github.com/googleapis/java-datastore/issues/1114) ) ( [7f58868](https://github.com/googleapis/java-datastore/commit/7f588682212e1a8f7e27d4cacb5995c0c129c090) )

## June 20, 2023

Announcement

[`  OR  ` queries](/datastore/docs/concepts/queries#composite_filters) are now supported at the [General Availability level](https://cloud.google.com/products/#product-launch-stages) .

## June 19, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.15.0](https://github.com/googleapis/java-datastore/compare/v2.14.7...v2.15.0) (2023-06-09)

##### Features

  - Multiple dbs support ( [\#1102](https://github.com/googleapis/java-datastore/issues/1102) ) ( [7887f32](https://github.com/googleapis/java-datastore/commit/7887f3255cba4dedd7b4f369d77a3279d903127f) )

##### Bug Fixes

  - Add some missing annotations and fix equals/hashcode for DatastoreOptions ( [\#1106](https://github.com/googleapis/java-datastore/issues/1106) ) ( [c4a79ef](https://github.com/googleapis/java-datastore/commit/c4a79effa83c5fdb7ad8db15ae52e2c70db238bc) )

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.11.0 ( [\#1104](https://github.com/googleapis/java-datastore/issues/1104) ) ( [fc9b091](https://github.com/googleapis/java-datastore/commit/fc9b09103a1bfbb238b22102dcf2b889292658ce) )

## May 23, 2023

Feature

Support for the [asia-south2 (Delhi)](/datastore/docs/locations#location-r) region.

## May 01, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.14.5](https://github.com/googleapis/java-datastore/compare/v2.14.4...v2.14.5) (2023-04-27)

##### Bug Fixes

  - Using namespace from DatastoreOptions if aggregation query is not configured with one. ( [\#1055](https://github.com/googleapis/java-datastore/issues/1055) ) ( [ac21ef6](https://github.com/googleapis/java-datastore/commit/ac21ef6cff5308fb17990a768100d1b2ee4c3654) ), closes [\#1054](https://github.com/googleapis/java-datastore/issues/1054)

#### [2.14.4](https://github.com/googleapis/java-datastore/compare/v2.14.3...v2.14.4) (2023-04-26)

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.8.0 ( [\#1052](https://github.com/googleapis/java-datastore/issues/1052) ) ( [412be61](https://github.com/googleapis/java-datastore/commit/412be617db28a97d38883bd6e26ddbc7d1c434fa) )
  - Update dependency org.junit.vintage:junit-vintage-engine to v5.9.3 ( [\#1056](https://github.com/googleapis/java-datastore/issues/1056) ) ( [2a871e2](https://github.com/googleapis/java-datastore/commit/2a871e25436a8812bc2f691c6462675b88976afc) )

##### Documentation

  - Remove `  @BetaApi  ` annotations for count aggregations ( [\#1051](https://github.com/googleapis/java-datastore/issues/1051) ) ( [b8bdaa2](https://github.com/googleapis/java-datastore/commit/b8bdaa23f165f6bcb5a891ef2437ffdd7ce8aa4c) )

## April 24, 2023

Feature

[`  count()  ` queries](https://cloud.google.com/datastore/docs/aggregation-queries) are now supported at the [General Availability level](https://cloud.google.com/products/#product-launch-stages) .

## April 17, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [7.5.1](https://github.com/googleapis/nodejs-datastore/compare/v7.5.0...v7.5.1) (2023-04-11)

##### Bug Fixes

  - Allow user to set custom endpoints ( [\#1101](https://github.com/googleapis/nodejs-datastore/issues/1101) ) ( [e79fa49](https://github.com/googleapis/nodejs-datastore/commit/e79fa49f753984e34b63538005f29ab7efb7695e) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.14.3](https://github.com/googleapis/java-datastore/compare/v2.14.2...v2.14.3) (2023-04-13)

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.7.0 ( [\#1044](https://github.com/googleapis/java-datastore/issues/1044) ) ( [3ecd20a](https://github.com/googleapis/java-datastore/commit/3ecd20a1c8575855dfb6c7b70d9f4a98a8e92591) )
  - Update dependency org.graalvm.buildtools:junit-platform-native to v0.9.21 ( [\#1045](https://github.com/googleapis/java-datastore/issues/1045) ) ( [d18ff7c](https://github.com/googleapis/java-datastore/commit/d18ff7c4738efe3cc7d43966fb1f3ec8733af3b6) )
  - Update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.21 ( [\#1046](https://github.com/googleapis/java-datastore/issues/1046) ) ( [0d3f78e](https://github.com/googleapis/java-datastore/commit/0d3f78ec05f8a4a6f6d3a89917e1d417740bb883) )

## April 14, 2023

Feature

The Firestore in Datastore mode documentation has been updated to include guidance on using regional endpoints. For details, see [Regional endpoints](/datastore/docs/regional-endpoints) .

## April 03, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.15.1](https://github.com/googleapis/python-datastore/compare/v2.15.0...v2.15.1) (2023-03-24)

##### Documentation

  - Fix formatting of request arg in docstring ( [\#428](https://github.com/googleapis/python-datastore/issues/428) ) ( [da86a02](https://github.com/googleapis/python-datastore/commit/da86a02744f02c34d9cf1c83ea20a4ca2bbde232) )
  - Improve query API documentation ( [\#430](https://github.com/googleapis/python-datastore/issues/430) ) ( [915daf5](https://github.com/googleapis/python-datastore/commit/915daf5443c74953f9d531c2bf2029e4a8e87d47) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.14.2](https://github.com/googleapis/java-datastore/compare/v2.14.1...v2.14.2) (2023-03-29)

##### Documentation

  - Adds OR filter sample ( [\#1032](https://github.com/googleapis/java-datastore/issues/1032) ) ( [e319efa](https://github.com/googleapis/java-datastore/commit/e319efa402539f0297179d270aa8c8f50e6e3e93) )

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.6.0 ( [\#1035](https://github.com/googleapis/java-datastore/issues/1035) ) ( [b2f4cb3](https://github.com/googleapis/java-datastore/commit/b2f4cb361afb1398b10edc0fcfe744b414926e07) )
  - Update gapic-generator-java to 2.16.0 ( [8c96c55](https://github.com/googleapis/java-datastore/commit/8c96c555159d48f1dc6d53616f0412f60e3095d7) )

## March 29, 2023

Change

Firestore in Datastore mode no longer limits the number of entities that can be passed to a `  Commit  ` operation. Previously, the limit was 500. [The limit for request size](/datastore/docs/concepts/limits#limits) still applies.

## March 24, 2023

Feature

[`  OR  ` queries](/datastore/docs/concepts/queries#composite_filters) now available in [Preview](https://cloud.google.com/products/#product-launch-stages) .

## March 20, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-ndb](https://github.com/googleapis/python-ndb)

#### [2.1.1](https://github.com/googleapis/python-ndb/compare/v2.1.0...v2.1.1) (2023-02-28)

##### Bug Fixes

  - Query options were not respecting use\_cache ( [\#873](https://github.com/googleapis/python-ndb/issues/873) ) ( [802d88d](https://github.com/googleapis/python-ndb/commit/802d88d108969cba02437f55e5858556221930f3) ), closes [\#752](https://github.com/googleapis/python-ndb/issues/752)

##### Documentation

  - Note that we support Python 3.11 in CONTRIBUTING file ( [\#872](https://github.com/googleapis/python-ndb/issues/872) ) ( [982ee5f](https://github.com/googleapis/python-ndb/commit/982ee5f9e768c6f7f5ef19bf6fe9e646e4e08e1f) )
  - Use cached versions of Cloud objects.inv files ( [\#863](https://github.com/googleapis/python-ndb/issues/863) ) ( [4471e2f](https://github.com/googleapis/python-ndb/commit/4471e2f11757be280266779544c59c90222b8184) ), closes [\#862](https://github.com/googleapis/python-ndb/issues/862)

## March 13, 2023

Feature

Support for the [`  europe-west4  ` (Netherlands)](/datastore/docs/locations) region.

## March 06, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.14.0](https://github.com/googleapis/python-datastore/compare/v2.13.2...v2.14.0) (2023-02-28)

##### Features

  - Enable "rest" transport in Python for services supporting numeric enums ( [6785908](https://github.com/googleapis/python-datastore/commit/678590808a0867dbb2c2002c1ead39586d61be86) )

##### Documentation

  - Minor documentation formatting and cleanup ( [6785908](https://github.com/googleapis/python-datastore/commit/678590808a0867dbb2c2002c1ead39586d61be86) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.13.6](https://github.com/googleapis/java-datastore/compare/v2.13.5...v2.13.6) (2023-03-02)

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.4.0 ( [\#1001](https://github.com/googleapis/java-datastore/issues/1001) ) ( [a230e03](https://github.com/googleapis/java-datastore/commit/a230e030fadc11c72f6ced51e566d59439bc1c6e) )

## February 27, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [7.3.2](https://github.com/googleapis/nodejs-datastore/compare/v7.3.1...v7.3.2) (2023-02-17)

##### Bug Fixes

  - Allow filtering null values ( [\#1067](https://github.com/googleapis/nodejs-datastore/issues/1067) ) ( [b89fa21](https://github.com/googleapis/nodejs-datastore/commit/b89fa211b366ec3e24ea5b2c8deeb90c695aa0df) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.13.5](https://github.com/googleapis/java-datastore/compare/v2.13.4...v2.13.5) (2023-02-17)

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.3.0 ( [\#994](https://github.com/googleapis/java-datastore/issues/994) ) ( [ce8df48](https://github.com/googleapis/java-datastore/commit/ce8df48ca03e561642e996f9a022b5edd5cb76d9) )
  - Update dependency org.graalvm.buildtools:junit-platform-native to v0.9.20 ( [\#989](https://github.com/googleapis/java-datastore/issues/989) ) ( [f71ccd9](https://github.com/googleapis/java-datastore/commit/f71ccd94c5ed7c01f388d31dda17387d13496547) )
  - Update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.20 ( [\#990](https://github.com/googleapis/java-datastore/issues/990) ) ( [5e984c8](https://github.com/googleapis/java-datastore/commit/5e984c87fc95e18fb9a43ebd8d5dbafe7090c1cf) )

## February 20, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [7.3.1](https://github.com/googleapis/nodejs-datastore/compare/v7.3.0...v7.3.1) (2023-02-17)

##### Bug Fixes

  - **deps:** Roll back dependency @google-cloud/datastore to ^7.2.0 ( [\#1069](https://github.com/googleapis/nodejs-datastore/issues/1069) ) ( [1677c53](https://github.com/googleapis/nodejs-datastore/commit/1677c53b612799a90c455636ac19e081ff3730b3) )

#### [7.3.0](https://github.com/googleapis/nodejs-datastore/compare/v7.2.0...v7.3.0) (2023-02-16)

## February 13, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [7.2.0](https://github.com/googleapis/nodejs-datastore/compare/v7.1.0...v7.2.0) (2023-02-09)

##### Features

  - Add dynamic routing header annotation to DatastoreV1 ( [b023ab4](https://github.com/googleapis/nodejs-datastore/commit/b023ab47146159c32ebc64dd09da681ad09c4081) )
  - Added Snooze API support ( [b023ab4](https://github.com/googleapis/nodejs-datastore/commit/b023ab47146159c32ebc64dd09da681ad09c4081) )
  - Added SuggestConversationSummary RPC ( [b023ab4](https://github.com/googleapis/nodejs-datastore/commit/b023ab47146159c32ebc64dd09da681ad09c4081) )
  - New transaction options for datastoreV1 ( [b023ab4](https://github.com/googleapis/nodejs-datastore/commit/b023ab47146159c32ebc64dd09da681ad09c4081) )

##### Bug Fixes

  - **deps:** Update dependency sinon to v15 ( [\#1020](https://github.com/googleapis/nodejs-datastore/issues/1020) ) ( [a61258c](https://github.com/googleapis/nodejs-datastore/commit/a61258c92354df5a62cf6e7d6977f8f83bfd907f) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.13.4](https://github.com/googleapis/java-datastore/compare/v2.13.3...v2.13.4) (2023-02-06)

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.2.0 ( [\#975](https://github.com/googleapis/java-datastore/issues/975) ) ( [f94bd37](https://github.com/googleapis/java-datastore/commit/f94bd3784686fc98fe90af4e74ea0afd040c7db4) )

## January 30, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.13.2](https://github.com/googleapis/python-datastore/compare/v2.13.1...v2.13.2) (2023-01-23)

##### Bug Fixes

  - Fix system test using utc timezone ( [\#406](https://github.com/googleapis/python-datastore/issues/406) ) ( [93537ef](https://github.com/googleapis/python-datastore/commit/93537ef83e9b0b9a2b367b863eb57c22862a9bde) )

#### [2.13.1](https://github.com/googleapis/python-datastore/compare/v2.13.0...v2.13.1) (2023-01-20)

##### Bug Fixes

  - Add context manager return types ( [9cec031](https://github.com/googleapis/python-datastore/commit/9cec031e7da6c97853e13c72f2e434f924e59743) )

##### Documentation

  - Add documentation for enums ( [9cec031](https://github.com/googleapis/python-datastore/commit/9cec031e7da6c97853e13c72f2e434f924e59743) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.13.3](https://github.com/googleapis/java-datastore/compare/v2.13.2...v2.13.3) (2023-01-23)

##### Bug Fixes

  - **java:** Skip fixing poms for special modules ( [\#1744](https://github.com/googleapis/java-datastore/issues/1744) ) ( [\#964](https://github.com/googleapis/java-datastore/issues/964) ) ( [c89b27a](https://github.com/googleapis/java-datastore/commit/c89b27ac6a7791312f61558515d89baffde40bdf) )

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.1.2 ( [\#966](https://github.com/googleapis/java-datastore/issues/966) ) ( [78e9e8e](https://github.com/googleapis/java-datastore/commit/78e9e8e74163f4c8bd7e1d42540e609a86a99769) )

## January 23, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Node.js

### Changes for [@google-cloud/datastore](https://github.com/googleapis/nodejs-datastore)

#### [7.1.0](https://github.com/googleapis/nodejs-datastore/compare/v7.0.0...v7.1.0) (2023-01-18)

##### Features

  - Add datastore aggregation query APIs ( [\#1008](https://github.com/googleapis/nodejs-datastore/issues/1008) ) ( [d5c2cb1](https://github.com/googleapis/nodejs-datastore/commit/d5c2cb1f0725f3cce1dde5b80ac7aff55b605f9a) )
  - Add the count aggregate function ( [\#972](https://github.com/googleapis/nodejs-datastore/issues/972) ) ( [76adfc6](https://github.com/googleapis/nodejs-datastore/commit/76adfc6db03a4196999a8d510c0ab1ca15218f24) )
  - Snapshot reads ( [\#963](https://github.com/googleapis/nodejs-datastore/issues/963) ) ( [0ecca86](https://github.com/googleapis/nodejs-datastore/commit/0ecca862fd93fc668a3dd3f5c93c54724e43f055) )
  - Support regapic LRO ( [\#957](https://github.com/googleapis/nodejs-datastore/issues/957) ) ( [99778fb](https://github.com/googleapis/nodejs-datastore/commit/99778fb5e031eadd067b1ae9be0f910985966956) )

##### Bug Fixes

  - Allow passing gax instance to client constructor ( [\#974](https://github.com/googleapis/nodejs-datastore/issues/974) ) ( [386b9c7](https://github.com/googleapis/nodejs-datastore/commit/386b9c735d57ce23f004ba3e9b1eb9a9377622dc) )
  - Better support for fallback mode ( [\#967](https://github.com/googleapis/nodejs-datastore/issues/967) ) ( [0447d87](https://github.com/googleapis/nodejs-datastore/commit/0447d87ec162d64988d47e2fb21715dea78b6720) )
  - Bring back LRO mixin ( [\#1009](https://github.com/googleapis/nodejs-datastore/issues/1009) ) ( [1d8de5f](https://github.com/googleapis/nodejs-datastore/commit/1d8de5f6bc5015dadd4be635748e799f05bfd325) )
  - Change import long to require ( [\#968](https://github.com/googleapis/nodejs-datastore/issues/968) ) ( [5e710f2](https://github.com/googleapis/nodejs-datastore/commit/5e710f2c47001114ad087084507ad6d494143f1b) )
  - **deps:** Update dependency @google-cloud/promisify to v3 ( [\#942](https://github.com/googleapis/nodejs-datastore/issues/942) ) ( [7b35856](https://github.com/googleapis/nodejs-datastore/commit/7b35856b0568571d5bcad70b2464344e6c06a4cb) )
  - **deps:** Use google-gax v3.5.2 ( [\#1013](https://github.com/googleapis/nodejs-datastore/issues/1013) ) ( [1753eae](https://github.com/googleapis/nodejs-datastore/commit/1753eae467bff477e7991f74acbe3000656a955f) )
  - Do not import the whole google-gax from proto JS ( [\#1553](https://github.com/googleapis/nodejs-datastore/issues/1553) ) ( [\#973](https://github.com/googleapis/nodejs-datastore/issues/973) ) ( [9550bbc](https://github.com/googleapis/nodejs-datastore/commit/9550bbcc10912ca28b64a89153f3ae8e7862d939) )
  - Preserve default values in x-goog-request-params header ( [\#979](https://github.com/googleapis/nodejs-datastore/issues/979) ) ( [2b80e1e](https://github.com/googleapis/nodejs-datastore/commit/2b80e1ef691a340ed15e3105983cd34983b57cb1) )
  - Regenerated protos JS and TS definitions ( [\#1016](https://github.com/googleapis/nodejs-datastore/issues/1016) ) ( [d0ae656](https://github.com/googleapis/nodejs-datastore/commit/d0ae656ca83fbad0be5659d8d4516d8bde879a28) )
  - Remove pip install statements ( [\#1546](https://github.com/googleapis/nodejs-datastore/issues/1546) ) ( [\#970](https://github.com/googleapis/nodejs-datastore/issues/970) ) ( [2225fc7](https://github.com/googleapis/nodejs-datastore/commit/2225fc7753086243778c240a444c4940c29c5499) )
  - Use google-gax v3.3.0 ( [9550bbc](https://github.com/googleapis/nodejs-datastore/commit/9550bbcc10912ca28b64a89153f3ae8e7862d939) )

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.13.0](https://github.com/googleapis/python-datastore/compare/v2.12.0...v2.13.0) (2023-01-14)

##### Features

  - Add dynamic routing header annotation to DatastoreV1 ( [\#400](https://github.com/googleapis/python-datastore/issues/400) ) ( [1043ba3](https://github.com/googleapis/python-datastore/commit/1043ba3638434657226c176f8e714f5dc476d1f5) )
  - New transaction options for datastoreV1 ( [\#402](https://github.com/googleapis/python-datastore/issues/402) ) ( [906d026](https://github.com/googleapis/python-datastore/commit/906d026920abb0e7e44b9309a7c37254159b95ee) )

## January 16, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.12.0](https://github.com/googleapis/python-datastore/compare/v2.11.1...v2.12.0) (2023-01-10)

##### Features

  - Add support for python 3.11 ( [\#396](https://github.com/googleapis/python-datastore/issues/396) ) ( [19aca56](https://github.com/googleapis/python-datastore/commit/19aca5608af28d0623fa1d43616b355b019fd18e) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.13.2](https://github.com/googleapis/java-datastore/compare/v2.13.1...v2.13.2) (2023-01-10)

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.1.1 ( [\#953](https://github.com/googleapis/java-datastore/issues/953) ) ( [fdffe1e](https://github.com/googleapis/java-datastore/commit/fdffe1e6b84fa58d7bf4210016d814642cbd45a2) )
  - Update dependency com.google.errorprone:error\_prone\_core to v2.18.0 ( [\#951](https://github.com/googleapis/java-datastore/issues/951) ) ( [ac5c83e](https://github.com/googleapis/java-datastore/commit/ac5c83e03f3ea1ef6a66373b80858cd68dda0c80) )
  - Update dependency org.junit.vintage:junit-vintage-engine to v5.9.2 ( [\#954](https://github.com/googleapis/java-datastore/issues/954) ) ( [b0b72bb](https://github.com/googleapis/java-datastore/commit/b0b72bb8ba3c6382f3d5883cd302a0d0756ccb71) )

## January 09, 2023

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.11.1](https://github.com/googleapis/python-datastore/compare/v2.11.0...v2.11.1) (2022-12-09)

##### Bug Fixes

  - **deps:** Require google-api-core \>=1.34.0, \>=2.11.0 ( [6f6bb63](https://github.com/googleapis/python-datastore/commit/6f6bb63219ac4369d16d39d5ec7b22bffe59c48f) )
  - Drop usage of pkg\_resources ( [6f6bb63](https://github.com/googleapis/python-datastore/commit/6f6bb63219ac4369d16d39d5ec7b22bffe59c48f) )
  - Fix timeout default values ( [6f6bb63](https://github.com/googleapis/python-datastore/commit/6f6bb63219ac4369d16d39d5ec7b22bffe59c48f) )

##### Documentation

  - **samples:** Snippetgen should call await on the operation coroutine before calling result ( [6f6bb63](https://github.com/googleapis/python-datastore/commit/6f6bb63219ac4369d16d39d5ec7b22bffe59c48f) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.13.1](https://github.com/googleapis/java-datastore/compare/v2.13.0...v2.13.1) (2023-01-03)

##### Dependencies

  - Update dependency com.google.errorprone:error\_prone\_core to v2.17.0 ( [\#944](https://github.com/googleapis/java-datastore/issues/944) ) ( [b0fd082](https://github.com/googleapis/java-datastore/commit/b0fd082f34d642f450d51e0c732daa3023fc57a4) )
  - Update dependency org.easymock:easymock to v5.1.0 ( [\#945](https://github.com/googleapis/java-datastore/issues/945) ) ( [7774aac](https://github.com/googleapis/java-datastore/commit/7774aaca4bb99bd5114002a511981dc6992b00f4) )

## December 19, 2022

Feature

Support for the [`  australia-southeast2  ` (Melbourne)](/datastore/docs/locations) region.

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-ndb](https://github.com/googleapis/python-ndb)

#### [2.1.0](https://github.com/googleapis/python-ndb/compare/v2.0.0...v2.1.0) (2022-12-15)

##### Features

  - Support client\_options for clients ( [\#815](https://github.com/googleapis/python-ndb/issues/815) ) ( [6f94f40](https://github.com/googleapis/python-ndb/commit/6f94f40dfcd6f10e3cec979e4eb2b83408c66a30) )

##### Bug Fixes

  - **zlib:** Accomodate different Zlib compression levels ( [\#852](https://github.com/googleapis/python-ndb/issues/852) ) ( [c1ab83b](https://github.com/googleapis/python-ndb/commit/c1ab83b9581b3d4d10dc7d2508b1c93b14e3c31a) )

## December 12, 2022

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-ndb](https://github.com/googleapis/python-ndb)

#### [2.0.0](https://github.com/googleapis/python-ndb/compare/v1.12.0...v2.0.0) (2022-12-06)

##### ⚠ BREAKING CHANGES

  - **dependencies:** Upgrade to google-cloud-datastore \>= 2.7.2

##### Features

  - **dependencies:** Upgrade to google-cloud-datastore \>= 2.7.2 ( [12bbcb5](https://github.com/googleapis/python-ndb/commit/12bbcb548c47803406246d6e3cf55cd947b1500a) )

##### Bug Fixes

  - Correct access to SerializeToString, CopyFrom, and MergeFromString ( [12bbcb5](https://github.com/googleapis/python-ndb/commit/12bbcb548c47803406246d6e3cf55cd947b1500a) )
  - Fix enum namespaces ( [12bbcb5](https://github.com/googleapis/python-ndb/commit/12bbcb548c47803406246d6e3cf55cd947b1500a) )
  - Update API capitalization/casing ( [12bbcb5](https://github.com/googleapis/python-ndb/commit/12bbcb548c47803406246d6e3cf55cd947b1500a) )
  - Update datastore stub creation ( [12bbcb5](https://github.com/googleapis/python-ndb/commit/12bbcb548c47803406246d6e3cf55cd947b1500a) )
  - Update module imports ( [12bbcb5](https://github.com/googleapis/python-ndb/commit/12bbcb548c47803406246d6e3cf55cd947b1500a) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.13.0](https://github.com/googleapis/java-datastore/compare/v2.12.5...v2.13.0) (2022-12-06)

##### Features

  - Next release from main branch is 2.13.0 ( [\#917](https://github.com/googleapis/java-datastore/issues/917) ) ( [1f12435](https://github.com/googleapis/java-datastore/commit/1f1243577cbdc206b6a0bfcde818411eb1b806ad) )

##### Bug Fixes

  - [\#355](https://github.com/googleapis/java-datastore/issues/355) Explicitly passing --project argument when starting emulator ( [\#923](https://github.com/googleapis/java-datastore/issues/923) ) ( [ef4065d](https://github.com/googleapis/java-datastore/commit/ef4065d233b968f58a34673aa53d39f60a013e2d) )

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.1.0 ( [\#932](https://github.com/googleapis/java-datastore/issues/932) ) ( [1dbcea7](https://github.com/googleapis/java-datastore/commit/1dbcea73827961148800c1ec8e87065dbceb6c88) )
  - Update dependency org.graalvm.buildtools:junit-platform-native to v0.9.18 ( [\#924](https://github.com/googleapis/java-datastore/issues/924) ) ( [625e896](https://github.com/googleapis/java-datastore/commit/625e89685172ae546a813f5f7184223d01fbb0ac) )
  - Update dependency org.graalvm.buildtools:junit-platform-native to v0.9.19 ( [\#930](https://github.com/googleapis/java-datastore/issues/930) ) ( [77285be](https://github.com/googleapis/java-datastore/commit/77285be97fbd6bca1ada35202842238e306dd8dc) )
  - Update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.18 ( [\#925](https://github.com/googleapis/java-datastore/issues/925) ) ( [0c7539d](https://github.com/googleapis/java-datastore/commit/0c7539d736ec993d7bb0531d7cd4dab1b08487a0) )
  - Update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.19 ( [\#931](https://github.com/googleapis/java-datastore/issues/931) ) ( [40b4011](https://github.com/googleapis/java-datastore/commit/40b4011e3a826a91e33541efdecb05f0e129f87c) )

## December 07, 2022

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Go

### Changes for [datastore/admin/apiv1](https://github.com/googleapis/google-cloud-go/tree/main/datastore/admin/apiv1)

#### [1.10.0](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.9.0...datastore/v1.10.0) (2022-11-29)

##### Features

  - **datastore:** start generating proto stubs ( [eed371e](https://github.com/googleapis/google-cloud-go/commit/eed371e9b1639c81663c6858db119fb87a126454) )

### Python

### Changes for [google-cloud-ndb](https://github.com/googleapis/python-ndb)

#### [1.12.0](https://github.com/googleapis/python-ndb/compare/v1.11.2...v1.12.0) (2022-11-29)

##### Bug Fixes

  - Drop Python 2 support ( [90efd77](https://github.com/googleapis/python-ndb/commit/90efd77633c97f530088dc3f079547ef4eefd796) )
  - Drop Python 3.6 support ( [\#829](https://github.com/googleapis/python-ndb/issues/829) ) ( [b110199](https://github.com/googleapis/python-ndb/commit/b1101994a34f70804027ea0c8a1b9f276d260756) )
  - **model:** Ensure repeated props have same kind when converting from ds ( [\#824](https://github.com/googleapis/python-ndb/issues/824) ) ( [29f5a85](https://github.com/googleapis/python-ndb/commit/29f5a853174857545e225fe2f0c682dfa0bc3884) )

##### Documentation

  - Add note in Django middleware documentation that it is unimplemented ( [\#805](https://github.com/googleapis/python-ndb/issues/805) ) ( [aa7621d](https://github.com/googleapis/python-ndb/commit/aa7621dba3b5c32141cdcb1d07829a217bb8b0bd) )
  - Add note that ProtoRPC message classes are unimplemented ( [\#819](https://github.com/googleapis/python-ndb/issues/819) ) ( [ae813e9](https://github.com/googleapis/python-ndb/commit/ae813e9995d103a45a0c7bc6b4c7bdc148c19c29) )
  - **context:** Note that several methods are no longer implemented. ( [\#821](https://github.com/googleapis/python-ndb/issues/821) ) ( [34c2c38](https://github.com/googleapis/python-ndb/commit/34c2c389d02f4692840631d34b6249b88867d725) )
  - **CONTRIBUTING:** Note the need for Redis/Memcached env vars in tests ( [\#838](https://github.com/googleapis/python-ndb/issues/838) ) ( [19f8415](https://github.com/googleapis/python-ndb/commit/19f84150ab06ae71e25ee48ba7f7285eb0402738) ), closes [\#836](https://github.com/googleapis/python-ndb/issues/836)
  - Fix bad import path in migration guide ( [\#827](https://github.com/googleapis/python-ndb/issues/827) ) ( [7b44961](https://github.com/googleapis/python-ndb/commit/7b449615629b5a08836ee17a8ab34eb8efbaed21) )
  - Fix typo in begin\_transaction docstring ( [\#822](https://github.com/googleapis/python-ndb/issues/822) ) ( [7fd3ed3](https://github.com/googleapis/python-ndb/commit/7fd3ed315d39a9a50746b00898b22edd3f7d1d0c) )
  - **README:** Syncronize supported version text with python-datastore ( [\#837](https://github.com/googleapis/python-ndb/issues/837) ) ( [316f959](https://github.com/googleapis/python-ndb/commit/316f95913f2dca12f314e429bbe8bd2582bc1c0f) )
  - **tasklets:** Fix Py2-style print statement ( [\#840](https://github.com/googleapis/python-ndb/issues/840) ) ( [0ebfaed](https://github.com/googleapis/python-ndb/commit/0ebfaedc48911b57d0cb23584a2a84c31a92d06a) )

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.11.0](https://github.com/googleapis/python-datastore/compare/v2.10.0...v2.11.0) (2022-11-30)

##### Features

  - Support "limit" in count query. ( [\#384](https://github.com/googleapis/python-datastore/issues/384) ) ( [a4b666a](https://github.com/googleapis/python-datastore/commit/a4b666a4a11b04903cf7a48f74e525205d13250e) )

## November 21, 2022

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-ndb](https://github.com/googleapis/python-ndb)

#### [1.12.0rc1](https://github.com/googleapis/python-ndb/compare/v1.11.2...v1.12.0rc1) (2022-11-17)

##### Bug Fixes

  - Drop Python 2 support ( [90efd77](https://github.com/googleapis/python-ndb/commit/90efd77633c97f530088dc3f079547ef4eefd796) )
  - Drop Python 3.6 support ( [\#829](https://github.com/googleapis/python-ndb/issues/829) ) ( [b110199](https://github.com/googleapis/python-ndb/commit/b1101994a34f70804027ea0c8a1b9f276d260756) )
  - **model:** Ensure repeated props have same kind when converting from ds ( [\#824](https://github.com/googleapis/python-ndb/issues/824) ) ( [29f5a85](https://github.com/googleapis/python-ndb/commit/29f5a853174857545e225fe2f0c682dfa0bc3884) )

##### Documentation

  - Add note in Django middleware documentation that it is unimplemented ( [\#805](https://github.com/googleapis/python-ndb/issues/805) ) ( [aa7621d](https://github.com/googleapis/python-ndb/commit/aa7621dba3b5c32141cdcb1d07829a217bb8b0bd) )
  - Add note that ProtoRPC message classes are unimplemented ( [\#819](https://github.com/googleapis/python-ndb/issues/819) ) ( [ae813e9](https://github.com/googleapis/python-ndb/commit/ae813e9995d103a45a0c7bc6b4c7bdc148c19c29) )
  - **context:** Note that several methods are no longer implemented. ( [\#821](https://github.com/googleapis/python-ndb/issues/821) ) ( [34c2c38](https://github.com/googleapis/python-ndb/commit/34c2c389d02f4692840631d34b6249b88867d725) )
  - **CONTRIBUTING:** Note the need for Redis/Memcached env vars in tests ( [\#838](https://github.com/googleapis/python-ndb/issues/838) ) ( [19f8415](https://github.com/googleapis/python-ndb/commit/19f84150ab06ae71e25ee48ba7f7285eb0402738) ), closes [\#836](https://github.com/googleapis/python-ndb/issues/836)
  - Fix bad import path in migration guide ( [\#827](https://github.com/googleapis/python-ndb/issues/827) ) ( [7b44961](https://github.com/googleapis/python-ndb/commit/7b449615629b5a08836ee17a8ab34eb8efbaed21) )
  - Fix typo in begin\_transaction docstring ( [\#822](https://github.com/googleapis/python-ndb/issues/822) ) ( [7fd3ed3](https://github.com/googleapis/python-ndb/commit/7fd3ed315d39a9a50746b00898b22edd3f7d1d0c) )
  - **README:** Syncronize supported version text with python-datastore ( [\#837](https://github.com/googleapis/python-ndb/issues/837) ) ( [316f959](https://github.com/googleapis/python-ndb/commit/316f95913f2dca12f314e429bbe8bd2582bc1c0f) )

#### [1.11.2](https://github.com/googleapis/python-ndb/compare/v1.11.1...v1.11.2) (2022-06-03)

##### Documentation

  - fix changelog header to consistent size ( [\#773](https://github.com/googleapis/python-ndb/issues/773) ) ( [7bb4e5a](https://github.com/googleapis/python-ndb/commit/7bb4e5a7bf11061a546f21e6f57cf2937f7a3a9d) )

## November 07, 2022

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Go

### Changes for [datastore/admin/apiv1](https://github.com/googleapis/google-cloud-go/tree/main/datastore/admin/apiv1)

#### [1.9.0](https://github.com/googleapis/google-cloud-go/compare/datastore/v1.8.0...datastore/v1.9.0) (2022-10-26)

##### Features

  - **datastore:** Adds COUNT aggregation query ( [\#6714](https://github.com/googleapis/google-cloud-go/issues/6714) ) ( [27363ca](https://github.com/googleapis/google-cloud-go/commit/27363ca581e3ae38d3eff0174727429838fcb4ac) )
  - **datastore:** Adds snapshot reads ( [\#6755](https://github.com/googleapis/google-cloud-go/issues/6755) ) ( [9240741](https://github.com/googleapis/google-cloud-go/commit/924074139a086aec7f12572d05909ee0b54e21f5) )

##### Documentation

  - **datastore:** Adds emulator instructions ( [\#6928](https://github.com/googleapis/google-cloud-go/issues/6928) ) ( [553456a](https://github.com/googleapis/google-cloud-go/commit/553456a469662e8e14de13b55b4193740b21ff96) )

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.10.0](https://github.com/googleapis/python-datastore/compare/v2.9.0...v2.10.0) (2022-11-01)

##### Features

  - Support the Count aggregation query ( [\#368](https://github.com/googleapis/python-datastore/issues/368) ) ( [b400a9a](https://github.com/googleapis/python-datastore/commit/b400a9ac0d8f0c0da22fe92c2c229e2e90e21007) )

## October 31, 2022

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.12.3](https://github.com/googleapis/java-datastore/compare/v2.12.2...v2.12.3) (2022-10-24)

##### Dependencies

  - Update dependency org.easymock:easymock to v5.0.1 ( [\#896](https://github.com/googleapis/java-datastore/issues/896) ) ( [0382c3d](https://github.com/googleapis/java-datastore/commit/0382c3ddfcf13192e483e371ab470f2dd83607aa) )

## October 24, 2022

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.9.0](https://github.com/googleapis/python-datastore/compare/v2.8.2...v2.9.0) (2022-10-18)

##### Features

  - Add datastore aggregation query APIs ( [\#306](https://github.com/googleapis/python-datastore/issues/306) ) ( [96d98e5](https://github.com/googleapis/python-datastore/commit/96d98e5204d71dfeb9547052cbdd073292ae4c6a) )

##### Bug Fixes

  - **deps:** Allow protobuf 3.19.5 ( [\#372](https://github.com/googleapis/python-datastore/issues/372) ) ( [9305154](https://github.com/googleapis/python-datastore/commit/9305154e8853f9038506c86163dfb4cde36c0d8e) )

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.2.11](https://github.com/googleapis/java-datastore/compare/v2.2.10...v2.2.11) (2022-10-17)

##### Dependencies

  - Regenerating with new Protobuf (2.2.x) ( [\#873](https://github.com/googleapis/java-datastore/issues/873) ) ( [9b3d60b](https://github.com/googleapis/java-datastore/commit/9b3d60b55c5d79dcc96a47a680aee6828b84de80) )

#### [2.12.2](https://github.com/googleapis/java-datastore/compare/v2.12.1...v2.12.2) (2022-10-21)

##### Dependencies

  - Update dependency com.google.cloud:google-cloud-shared-dependencies to v3.0.5 ( [\#891](https://github.com/googleapis/java-datastore/issues/891) ) ( [1f32176](https://github.com/googleapis/java-datastore/commit/1f3217607b491db594cde2e7e767c8e50aa26eb1) )

#### [2.12.1](https://github.com/googleapis/java-datastore/compare/v2.12.0...v2.12.1) (2022-10-19)

##### Dependencies

  - Update dependency org.graalvm.buildtools:junit-platform-native to v0.9.16 ( [\#885](https://github.com/googleapis/java-datastore/issues/885) ) ( [c8b7559](https://github.com/googleapis/java-datastore/commit/c8b75595e74a33d29d972af8c463cf33c41ac02b) )
  - Update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.16 ( [\#886](https://github.com/googleapis/java-datastore/issues/886) ) ( [76df7ea](https://github.com/googleapis/java-datastore/commit/76df7eaadf1d27e1669a557039ac790a11c110b3) )

#### [2.12.0](https://github.com/googleapis/java-datastore/compare/v2.11.5...v2.12.0) (2022-10-17)

##### Features

  - Count API ( [\#823](https://github.com/googleapis/java-datastore/issues/823) ) ( [8c22e61](https://github.com/googleapis/java-datastore/commit/8c22e61f8a0307a59301259f83a16c8324fa1b6f) )

##### Dependencies

  - Update dependency com.google.errorprone:error\_prone\_core to v2.16 ( [\#872](https://github.com/googleapis/java-datastore/issues/872) ) ( [b2a72ca](https://github.com/googleapis/java-datastore/commit/b2a72ca407b1fa168c18b136e73932c8716fbdf6) )
  - Update dependency org.easymock:easymock to v5 ( [\#877](https://github.com/googleapis/java-datastore/issues/877) ) ( [ed816e2](https://github.com/googleapis/java-datastore/commit/ed816e20b605882a9cf2c637145597fdcd95f324) )
  - Update dependency org.graalvm.buildtools:junit-platform-native to v0.9.15 ( [\#878](https://github.com/googleapis/java-datastore/issues/878) ) ( [831a92b](https://github.com/googleapis/java-datastore/commit/831a92bdc1d3f81fb44ae8d17cad236a50234ea5) )
  - Update dependency org.graalvm.buildtools:native-maven-plugin to v0.9.15 ( [\#879](https://github.com/googleapis/java-datastore/issues/879) ) ( [76a187a](https://github.com/googleapis/java-datastore/commit/76a187a48cdc8d40fa233123894a36e11c590ca9) )

## October 21, 2022

Feature

[`  count()  ` queries](/datastore/docs/aggregation-queries) are now available in [Preview](https://cloud.google.com/products/#product-launch-stages) .

## October 17, 2022

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Python

### Changes for [google-cloud-datastore](https://github.com/googleapis/python-datastore)

#### [2.8.3](https://github.com/googleapis/python-datastore/compare/v2.8.2...v2.8.3) (2022-10-10)

##### Bug Fixes

  - **Deps:** Allow protobuf 3.19.5 ( [\#372](https://github.com/googleapis/python-datastore/issues/372) ) ( [9305154](https://github.com/googleapis/python-datastore/commit/9305154e8853f9038506c86163dfb4cde36c0d8e) )

#### [2.8.3](https://github.com/googleapis/python-datastore/compare/v2.8.2...v2.8.3) (2022-10-10)

##### Bug Fixes

  - **Deps:** Allow protobuf 3.19.5 ( [\#372](https://github.com/googleapis/python-datastore/issues/372) ) ( [9305154](https://github.com/googleapis/python-datastore/commit/9305154e8853f9038506c86163dfb4cde36c0d8e) )

## October 11, 2022

Feature

[Time-to-live (TTL) policies](https://cloud.google.com/datastore/docs/ttl) are now supported at the [General Availability level](https://cloud.google.com/products/#product-launch-stages) .

## September 30, 2022

Feature

**Note:** This feature has been disabled and moved to a future release.

In the Google Cloud console, updated the pages for editing an entity. See [Edit an entity in the console](/datastore/docs/editing_entity_console) .

## August 15, 2022

Libraries

A weekly digest of client library updates from across the [Cloud SDK](/sdk) .

### Java

### Changes for [google-cloud-datastore](https://github.com/googleapis/java-datastore)

#### [2.11.0](https://github.com/googleapis/java-datastore/compare/v2.10.1...v2.11.0) (2022-08-04)

##### Features

  - add database\_id field ( [\#802](https://github.com/googleapis/java-datastore/issues/802) ) ( [6ed09dd](https://github.com/googleapis/java-datastore/commit/6ed09dd44865639922156c85a441b7c6bb751df9) )

##### Documentation

  - **sample:** Add a top-level Datastore samples README ( [\#790](https://github.com/googleapis/java-datastore/issues/790) ) ( [d3884dc](https://github.com/googleapis/java-datastore/commit/d3884dce1b04f3143190e8cfbb084dd22fa6df15) )

##### Dependencies

  - update dependency com.google.cloud:google-cloud-shared-dependencies to v3 ( [\#805](https://github.com/googleapis/java-datastore/issues/805) ) ( [ad467ef](https://github.com/googleapis/java-datastore/commit/ad467ef55696dcb9bb2b340916216000aff6bcc8) )
  - update dependency com.google.errorprone:error\_prone\_core to v2.15.0 ( [\#810](https://github.com/googleapis/java-datastore/issues/810) ) ( [fc8cd15](https://github.com/googleapis/java-datastore/commit/fc8cd15a72a80109a519b0dcc1236a2606b41264) )
  - update dependency org.junit.vintage:junit-vintage-engine to v5.9.0 ( [\#804](https://github.com/googleapis/java-datastore/issues/804) ) ( [6caafd8](https://github.com/googleapis/java-datastore/commit/6caafd854278953de937a4a07c8ef163850ab9b0) )

## July 19, 2022

Feature

[Time-to-live (TTL) policies](https://cloud.google.com/datastore/docs/ttl) now available in [Preview](https://cloud.google.com/products/#product-launch-stages) .

## June 29, 2022

Feature

Not-equal (\!=), IN, and NOT\_IN query filters now available in all client libraries:

  - Java
  - Python
  - PHP
  - Node.js
  - C\#
  - Go
  - Ruby

**Note:** This feature is available for Firestore in Datastore mode. It is not available in Legacy Cloud Datastore.

## June 17, 2022

Feature

[Datastore now supports the not-equal ( `  !=  ` ), `  IN  ` and `  NOT_IN  ` query filters.](https://cloud.google.com/datastore/docs/concepts/queries#special_query_types) The filters are now available in the Google Cloud console and the following client libraries:

  - Java
  - Python
  - PHP
  - Node.js

**Note:** This feature is available for Firestore in Datastore mode. It is not available in Legacy Cloud Datastore.

## June 01, 2022

Feature

[Support for VPC Service Controls](/datastore/docs/securing-with-vpc-sc) is now available in **General Availability** .

## April 28, 2022

Feature

The `  datastore.databases.getMetadata  ` permission now supports custom Identity and Access Management roles. You can use custom roles with this permission to [unlink your database from App Engine](/datastore/docs/app-engine-requirement) .

## January 12, 2022

Feature

[Support for VPC Service Controls](/datastore/docs/securing-with-vpc-sc) is now available in [Preview](https://cloud.google.com/products/#product-launch-stages) .

## December 15, 2021

Feature

[Key Visualizer for Datastore](/datastore/docs/key-visualizer) is now generally available ( [GA](https://cloud.google.com/products#product-launch-stages) ).

## November 04, 2021

Feature

`  DATA_READ  ` and `  DATA_WRITE  ` Data Access audit logs are now supported at the [General Availability release level](https://cloud.google.com/products/#product-launch-stages) . See [Datastore audit logging information](/datastore/docs/audit-logging) .

## September 02, 2021

Feature

Added `  DATA_READ  ` and `  DATA_WRITE  ` Data Access audit logs. See [Firestore in Datastore mode audit logging information](/datastore/docs/audit-logging) . This feature is available in **Preview** .

## July 22, 2021

Change

**This feature was released on [September 2, 2021](#September_02_2021) .**

The `  DATA_READ  ` and `  DATA_WRITE  ` Data Access audit logs feature has been moved to a future release. It is not currently available.

## July 16, 2021

Feature

**This feature release was moved to [September 2, 2021](#September_02_2021) .**

Added `  DATA_READ  ` and `  DATA_WRITE  ` Data Access audit logs. See [Firestore in Datastore mode audit logging information](/datastore/docs/audit-logging) . This feature is available in **Preview** .

## June 15, 2021

Feature

Support for [Identity and Access Management custom roles](/datastore/docs/access/iam#custom-roles) .

## June 14, 2021

Feature

Support for the following additional locations:

  - `  asia-southeast1  ` Singapore
  - `  us-west1  ` Oregeon
  - `  asia-east1  ` Taiwan

See the [full list of locations](/datastore/docs/locations) .

## May 13, 2021

Feature

You can now [view recent import and export operations from the Google Cloud Console](/datastore/docs/export-import-entities#listing_all_long-running_operations) .

## April 13, 2021

Feature

Support for the [`  europe-central2  ` (Warsaw)](/datastore/docs/locations) region.

## September 16, 2020

Feature

You can now use the [`  goog-firestoremanaged  ` billing report label](/datastore/docs/export-import-entities#viewing_export_and_import_costs) to view costs related to export and import operations.

## September 14, 2020

Breaking

The `  gcloud datastore index create  ` and `  gcloud datastore index cleanup  ` commands now require gcloud version 279.0.0 or greater. To update the gcloud CLI, use the [`  gcloud components update  `](/sdk/docs/components#updating_components) command.

## June 08, 2020

Feature

Support for the [`  asia-southeast2  ` (Jakarta)](/datastore/docs/locations) region.

## April 20, 2020

Feature

Support for [`  us-west4  ` region (Las Vegas)](/datastore/docs/locations) .

## March 11, 2020

Feature

Support for [`  us-west3  ` (Salt Lake City) and `  asia-northeast3  ` (Seoul)](/datastore/docs/locations) .

## February 13, 2020

Feature

You can now [configure indexes with the REST API](/datastore/docs/configure-indexes-rest-api) .

## November 18, 2019

Feature

You can now [start managed export and import operations from the Google Cloud Console](/datastore/docs/export-import-entities#exporting_all_entities) .

## April 18, 2019

Feature

Support for [`  asia-northeast2  ` region (Osaka)](/datastore/docs/locations) .

## April 15, 2019

Feature

Support for [`  europe-west6  ` region (Zürich)](/datastore/docs/locations) .

## January 31, 2019

Feature

[Cloud Firestore is now Generally Available.](/firestore/docs/release-notes#january_31_2019) Cloud Firestore is the new version of Cloud Datastore and includes a backwards-compatible [Datastore mode](/firestore/docs/firestore-or-datastore#in_datastore_mode) .

If you intend to use the Cloud Datastore API in a new project, use Cloud Firestore in Datastore mode. Existing Cloud Datastore databases will be [automatically upgraded to Cloud Firestore in Datastore mode](/datastore/docs/upgrade-to-firestore) .

Except where noted, the Cloud Datastore documentation now describes behavior for Cloud Firestore in Datastore mode.

## October 22, 2018

Feature

Support for [`  asia-east2  ` region (Hong Kong)](/datastore/docs/locations) .

Change

Cloud Datastore will soon enforce IAM requirements for all App Engine apps, see [Cloud Datastore permissions for App Engine](/datastore/docs/activate#datastore-permissions-for-app-engine) . Previously, App Engine apps could always access Cloud Datastore instances in the same project.

Cloud Datastore IAM requirements for App Engine will apply to projects created after 09/03/2018 and will gradually rollout to existing projects. At a future date, all projects will enforce Cloud Datastore IAM requirements for App Engine.

## October 08, 2018

Feature

You can now create a [Cloud Firestore database in Datastore mode](/datastore/docs/firestore-or-datastore#choosing_a_database) . Datastore mode allows you to use Cloud Datastore client libraries with an improved Cloud Firestore storage layer, removing eventual consistency limitations.

If you have an existing Cloud Datastore project, see this page on the [automatic upgrade to Cloud Firestore](/datastore/docs/upgrade-to-firestore) .

## July 10, 2018

Feature

Support for [`  us-west2  ` region (Los Angeles)](/datastore/docs/locations) .

## February 28, 2018

Deprecated

The Cloud Datastore Administration API v1beta1 is now deprecated.

Deprecated

The Cloud Datastore Admin backup feature is being phased out in favor of the [managed export and import](/datastore/docs/export-import-entities) for Cloud Datastore. Please migrate to the managed export and import functionality at your earliest convenience. To help you make the transition, the Datastore Admin backup feature will continue to be available until February 28, 2019.

Feature

General Availability release of the [Cloud Datastore Administration API v1](/datastore/docs/reference/admin/rest/v1/projects) , previously in Beta. To learn more about using this service, see:

  - [Exporting and Importing Entities](/datastore/docs/export-import-entities)
  - [Scheduling an Export](/datastore/docs/schedule-export)

## January 30, 2018

Feature

When you begin a transaction with the Cloud Datastore Data API, you can now use a [`  TransactionOptions  `](/datastore/docs/reference/data/rest/v1/projects/beginTransaction#TransactionOptions) object to specify whether the transaction is read-only or read-write.

Change

Message [`  BeginTransactionRequest  `](/datastore/docs/reference/data/rest/v1/projects/beginTransaction) adds field `  transactionOptions  ` as part of the Data API.

Feature

When you begin a read-write transaction with the Cloud Datastore Data API, you can now specify a [`  previousTransaction  `](/datastore/docs/reference/data/rest/v1/projects/beginTransaction#ReadWrite) that you are retrying.

## January 10, 2018

Feature

Support for [`  northamerica-northeast1  ` region (Montréal)](/datastore/docs/locations) .

## October 31, 2017

Feature

Support for [`  asia-south1  ` region (Mumbai)](/datastore/docs/locations) .

## September 05, 2017

Feature

Support for [`  southamerica-east1  ` region (São Paulo)](/datastore/docs/locations) .

## August 30, 2017

Feature

Initial Beta release of the Cloud Datastore Administration API v1.

Additions to the API definition:

  - Methods for exporting and importing entities.
      - [export](/datastore/docs/reference/admin/rest/v1beta1/projects/export)
      - [import](/datastore/docs/reference/admin/rest/v1beta1/projects/import)
  - Methods for managing long-running operations.
      - [cancel](/datastore/docs/reference/rest/v1/projects.operations/cancel)
      - [delete](/datastore/docs/reference/rest/v1/projects.operations/delete)
      - [get](/datastore/docs/reference/rest/v1/projects.operations/get)
      - [list](/datastore/docs/reference/rest/v1/projects.operations/list)

Additions to the `  gcloud  ` command-line tool effective in [version 169.0.0](/sdk/docs/release-notes#16900_2017-08-30) :

  - `  gcloud beta datastore export  ` has been added to support exporting entities
  - `  gcloud beta datastore import  ` has been added to support importing entities
  - `  gcloud beta datastore operations cancel  ` has been added to support canceling long-running operations
  - `  gcloud beta datastore operations delete  ` has been added to support deleting long-running operations
  - `  gcloud beta datastore operations describe  ` has been added to support describing a completed long-running operation
  - `  gcloud beta datastore operations list  ` has been added to support listing active long-running operations

## August 01, 2017

Feature

Support for [`  europe-west3  ` region (Frankfurt)](/datastore/docs/locations) .

## July 18, 2017

Feature

Support for [`  australia-southeast1  ` region (Sydney)](/datastore/docs/locations) .

## June 06, 2017

Feature

Support for [`  europe-west2  ` region (London)](/datastore/docs/locations) .

## August 16, 2016

Change

Message `  EntityResult  ` adds field `  version  ` as part of API v1 and API v1beta3.

Feature

Initial release of Cloud Datastore API v1.

Change

Error handling in Cloud Datastore API v1:

  - Attempting to insert an entity that already exists will return error code `  ALREADY_EXISTS  ` . In v1beta3, it returned `  INVALID_ARGUMENT  ` .
  - Attempting to update an entity that does not exist will return error code `  NOT_FOUND  ` . In v1beta3, it returned `  INVALID_ARGUMENT  ` .

Deprecated

Because Cloud Datastore API v1 is released, Cloud Datastore API v1beta3 is now deprecated.

## April 01, 2016

Change

  - Initial release of Cloud Datastore API v1beta3.
  - Changes to the API definition:
      - The API is now defined in three proto files: `  entity.proto  ` , `  query.proto  ` , and `  datastore.proto  ` .
      - The proto files now use proto3 syntax:
          - Maps are used for several fields (see below for details).
          - All enums add a value with suffix `  _UNSPECIFIED  ` that is equal to 0.
          - `  oneof  ` is used to prevent setting mutually-exclusive fields:
              - Fields `  id  ` and `  name  ` in message `  PathElement  ` .
              - The value fields in message `  Value  ` .
              - Fields `  composite_filter  ` and `  property_filter  ` in type `  Filter  ` .
              - Fields `  value  ` and `  cursor  ` in message `  GqlQueryParameter  ` .
              - Fields `  upsert  ` , `  update  ` , `  upsert  ` , and `  delete  ` in message `  Mutation  ` .
      - All request messages add a top-level field `  project_id  ` . This field is populated automatically for requests made over HTTP.
      - Several repeated fields now have plural names:
          - In message `  CompositeFilter  ` , `  filter  ` is now `  filters  ` .
          - In message `  QueryResultBatch  ` , `  entity_result  ` is now `  entity_results  ` .
          - In message `  LookupRequest  ` , `  key  ` is now `  keys  ` .
          - In message `  AllocateIdsRequest  ` , `  key  ` is now `  keys  ` .
          - In message `  AllocateIdsResponse  ` , `  key  ` is now `  keys  ` .
      - The proto package name now includes the API version.
      - In message `  PartitionId  ` :
          - Field `  dataset_id  ` is now `  project_id  ` . `  project_id  ` never includes the app/project ID "prefix" (e.g. "s\~"). This fixes <https://github.com/GoogleCloudPlatform/google-cloud-datastore/issues/59> .
          - Field `  namespace  ` is now `  namespace_id  ` .
      - In message `  Key  ` , field `  path_element  ` is now `  path  ` .
      - In message `  Value  ` :
          - Null values are represented by explicitly setting field `  null_value  ` with type `  com.protobuf.NullValue  ` . This fixes <https://github.com/GoogleCloudPlatform/google-cloud-datastore/issues/41> .
          - Field `  timestamp_microseconds_value  ` is now `  timestamp_value  ` with type `  google.protobuf.Timestamp  ` . In JSON, the field `  dateTimeValue  ` is now `  timestampValue  ` . This field is still limited to microsecond precision.
          - Field `  blob_key_value  ` is removed. Values that previously populated that field in the v1beta1 or v1beta2 APIs will instead populate field `  string_value  ` in the v1beta3 API.
          - Field `  geo_point_value  ` of type `  google.type.LatLng  ` is added.
          - Repeated field `  list_value  ` is replaced with `  array_value  ` of type `  ArrayValue  ` .
          - Field `  indexed  ` , which defaulted to true, is now `  exclude_from_indexes  ` , which defaults to false.
      - Message `  Property  ` is removed. In message `  Entity  ` , repeated field `  property  ` is now field `  properties  ` which is a map from `  string  ` to `  Value  ` .
      - Message `  PropertyExpression  ` is now `  Projection  ` .
      - Message `  EntityResult  ` adds a field `  cursor  ` of type `  bytes  ` .
      - In message `  Query  ` :
          - Field `  group_by  ` is now `  distinct_on  ` .
          - Field `  limit  ` is now of type `  google.protobuf.Int32Value  ` .
      - In message `  PropertyExpression  ` , enum `  AggregationFunction  ` and field `  aggregation_function  ` are removed.
      - In messages `  CompositeFilter  ` and `  PropertyFilter  ` , field `  operator  ` is now `  op  ` .
      - In message `  GqlQuery  ` :
          - Field `  allow_literal  ` is now `  allow_literals  ` .
          - Repeated field `  name_arg  ` is now map field `  named_bindings  ` .
          - Field `  number_arg  ` is now `  positional_bindings  ` .
      - Message `  GqlQueryArg  ` is now `  GqlQueryParameter  ` . Field `  name  ` is removed.
      - Enum `  MoreResultsType  ` adds a new value `  MORE_RESULTS_AFTER_CURSOR  ` .
      - Message `  QueryResultBatch  ` adds field `  skipped_cursor  ` .
      - In message `  Mutation  ` :
          - A `  Mutation  ` now describes one change to one single entity. Its fields are no longer repeated.
          - Field `  insert_auto_id  ` is removed. `  insert  ` and `  update  ` mutations now support auto ID allocation.
          - Field `  force  ` is removed.
      - In message `  MutationResult  ` :
          - Field `  index_updates  ` is moved to message `  CommitResponse  ` .
          - Repeated field `  insert_auto_id_key  ` is now `  key  ` and is no longer repeated.
      - Message `  RunQueryResponse  ` adds field `  query  ` . When a `  RunQueryRequest  ` message sets field `  gql_query  ` , the `  RunQueryResponse  ` message sets field `  query  ` to the parsed form of the `  GqlQuery  ` message from the request.
      - In message `  BeginTransactionRequest  ` , enum `  IsolationLevel  ` and field `  isolation_level  ` are removed. All transactions are now serializable.
      - In message `  CommitRequest  ` , field `  mutation  ` is now repeated field `  mutations  ` .
      - In message `  CommitResponse  ` , field `  mutation_result  ` is now repeated field `  mutation_results  ` .
  - Changes to the JSON API:
      - Null values are now supported. This fixes <https://github.com/GoogleCloudPlatform/google-cloud-datastore/issues/41> .
      - Fields set to their default values are not included in responses, for example:
          - Fields `  found  ` , `  missing  ` , and `  deferred  ` in message to `  LookupResponse  ` are not included when they are empty.
          - Field `  entity_result  ` in message `  QueryResultBatch  ` is not included when it is empty.
          - Field `  skipped_results  ` in message `  QueryResultBatch  ` is not included when it is 0.
  - The API endpoint format has changed. For example, in v1beta2, a `  RunQuery  ` is sent to: `  https://www.googleapis.com/datastore/v1beta2/datasets/<dataset-id>/runQuery  ` In v1beta3, it is sent to: `  https://datastore.googleapis.com/v1beta3/projects/<project-id>:runQuery  `
  - Account domain restrictions no longer apply when accessing the API. This fixes <https://github.com/GoogleCloudPlatform/google-cloud-datastore/issues/19> .
  - Errors:
      - JSON errors add a `  status  ` field and remove the `  errors  ` list.
      - Errors resulting from requests with a content type of `  application/x-protobuf  ` are now a serialized `  google.rpc.Status  ` message.
  - Changes to GQL:
      - In synthetic literal `  KEY  ` , `  DATASET  ` is now `  PROJECT  ` .
      - The `  BLOBKEY  ` synthetic literal is removed.
      - The `  FIRST  ` aggregator is removed.
      - The `  GROUP BY  ` clause is replaced with `  DISTINCT ON  ` .
      - Fully-qualified property names are now supported.
      - Query filters on timestamps prior to the epoch are now supported.
  - Empty array values are now supported.
  - Indexing and querying properties inside of entity values is now supported. Values inside entity values are indexed by default.
  - Key normalization:
      - In `  Key  ` objects in `  RunQueryRequest  ` s, key normalization will never set `  partition_id.namespace_id  ` , as it previously did under some circumstances. If a key should reference that partition its `  partition_id.namespace_id  ` must be explicitly set.
      - `  Key  ` objects with empty `  path  ` and empty or unset `  partition_id  ` are no longer normalized.
  - Writes of foreign partition IDs may now fail if the foreign project is not in an active state. For this reason, use of foreign partition IDs is discouraged.
  - In a non-transactional `  Commit  ` requests, no two mutations may affect the same entity.
  - In transactional `  Commit  ` requests, mutations affecting the same entity are applied in the order in which they appear in the request. Certain sequences of mutations affecting the same entity are not permitted.
  - Field `  more_results  ` in message `  QueryResultBatch  ` is accurate in more cases. This fixes <https://github.com/GoogleCloudPlatform/google-cloud-datastore/issues/48> .
  - The typical number of results returned by a call to `  RunQuery  ` is smaller due to a change in server-side batching. As before, clients should not rely on the batch size and instead use cursors to continue queries.
  - Scope `  https://www.googleapis.com/auth/userinfo.email  ` is no longer required.
  - The API works for projects that have an App Engine domain restriction. This fixes <https://github.com/GoogleCloudPlatform/google-cloud-datastore/issues/19> .
  - `  gcd  ` tool:
      - Options `  -d  ` , `  --dataset_id  ` , and `  --dataset_id_override  ` are now `  -p  ` , `  --project_id  ` , and `  --project_id_override  ` , respectively.
      - Option `  --auth_mode  ` is removed. The `  updateindexes  ` and `  vacuumindexes  ` commands always use OAuth 2.0.
      - Option `  --auto_generate_indexes  ` is now `  --store_index_configuration_on_disk  ` .
      - Index configuration for new projects is now stored in a YAML file: `  <directory>/WEB-INF/index.yaml  ` . Index configuration for projects that previously used XML will continue to do so.

## September 01, 2013

Change

  - Initial release of Cloud Datastore API v1beta2.
  - Changes to the API:
      - `  BlindWrite  ` method merged into `  Commit  ` .
      - Added `  list_value  ` to `  Value  ` and changed `  value  ` to a non-repeated field in `  Property  ` .
      - In the JSON API, string constants are now uppercase and underscore-separated instead of camel-cased (e.g. `  LESS_THAN_OR_EQUAL  ` instead of `  lessThanOrEqual  ` ).
  - Changes to GQL:
      - New synthetic literals: `  BLOB  ` , `  BLOBKEY  ` , `  DATETIME  ` , `  KEY  ` .
      - Support for `  IS NULL  ` .
      - Fixed partition ID handling for binding arguments.
  - Fixed partition ID handling for query requests that include an explicit partition ID.
  - Fixed scopes in discovery document. This fixes <https://github.com/GoogleCloudPlatform/google-cloud-datastore/issues/9> .

## July 01, 2013

Change

  - GQL support.
  - Metadata query support.
  - `  gcd  ` tool:
      - Microsoft Windows support ( `  gcd.cmd  ` ).
      - Added testing mode option `  --testing  ` , which doesn't store data or index configuration on disk and supports fully-consistent non-ancestor queries. This option is useful for unit and integration tests.
      - More intuitive `  update_indexes  ` command (renamed to `  updateindexes  ` ).
      - New `  create  ` command and simplified `  start  ` command.
      - Improved integration with existing App Engine applications.

## May 01, 2013

Change

  - Initial public beta release (v1beta1) of the Cloud Datastore API.
