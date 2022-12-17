# releases.json

A specification for the releases.json data format.

## Introduction

This specification documents the `releases.json` file format, which is intended to be used by vendors to publish
information about various releases of the artifacts produced by them.

## Terms

**Product**: is an artifact produced by the vendor, typically a software or device.

**Release**: is a singular release made for a product. It is identified by its version string, which is specified without any `v` prefix.

**Release Cycle**: is a group of releases, typically grouped by their compatibility or closeness in variations.

**Support**: The expectation of receiving timely bug fixes for any defects in the product.

**Security Support**: The expectation of receiving security fixes (such as fixes for CVEs, security announcements etc) for a product.

**End-of-Life**: When a product reaches End-of-Life, no further updates are expected, including security fixes.

**Commercial Support**: Expectation of receiving fixes from a vendor on payment to a vendor - not necessarily first-party.

**Long-Term-Support**: A Long-Term-Support release cycle is expected to be maintained for a longer time period than usual releases.

**Active Support**: When a specific release cycle gets active development, for both bug fixes as well as feature development.

**Supported Release**: A release under a Release Cycle that has not yet reached End-of-Life.

## Specification

The releases.json file is expected to be located at `/.well-known/releases.json` on the primary website of the vendor. 
In case the primary website is a source-code repository, a top-level releases.json file can also be used in the repository.
To delegate updates to this file, a 302 redirect can be configured, and should be supported by any clients.

### Keys

```
# A list of various products offered by the vendor
products: [ 
  // An array of products
  // each specified as under.
],
// TODO: Decide Vendor/Supplier/....?
vendor: {
// TODO
}
```

### Product Specification

```json5
{
  name: "Product Name",
  // URL for the product, where more information can be found.
  url: ""
  // TODO: Specify this properly
  vcs: "",
  # URL where more information about the support policy can be found.
  policyURL: "https://example.com/support-information",
  // A list of supported versions, which is as per the `eol` dates.
  // This must match one of the latestVersion
  // TODO: Decide between supportedVersions or supportedReleases
  supportedReleases: [
    "5.2.3",
    "4.3.17"
  ],
  releaseCycles: [
    {
      // Release Cycle Identifier
      id: "5.2",
      // Other alternative idenfiers for this release cycle.
      // Helpful especially, when the product is distributed via alternative channels
      // and different identifiers are used across channels (such as platforms, countries etc).
      variants: ["05.2"],
      name: "5.2",
      // Long-term-support = true/false/YYYY-MM-DD
      // Use a date, if the release "enters" LTS on a specific date.
      // default: false
      lts: true,
      // optional, must belong to the release cycle.
      codename: "dragon",
      // Valid date in YYYY-MM-DD format
      // In case the release was staggered over time, the date of first
      // release should be used.
      releaseDate: 2022-04-01,
      // Latest version of the product under this release cycle
      latestVersion: "5.2.3",
      latestReleaseDate: 2022-12-16,
      // TODO: This is new, to provide separate links for both.
      link: "https://example.com/5.2",
      // A link where more information can be found about the latest version
      // This could be a changelog, or release notes, or the announcement URL
      latestLink: "https://example.com/5.2.3",
      // The EOL field denotes a release cycle as end-of-life
      // If the EOL was reached on a specific date, use YYYY-MM-DD
      // If the eol date is unavailable, but product is EOL, use true
      // Otherwise, set to false.
      // eol: true,
      // eol: false
      eol: 2024-12-01,
      
      // TODO: Decide on available/discontinued naming
      // Whether this release is still published and made available
      // via a primary non-archive source. 
      // For devices, this would imply the device is available in the market
      // for software products, they should be downloadable on the primary source.
      availability: true/false
      
      // Support Variants.
      // TODO: Find better name, maybe "supportVariants"?
      plans: {
        // Standard Keys that can be used here are:
        // 1. commercial
        // 2. extended
        // Non-standard keys can be used to denote separate plans.
        "commercial": {
          eol: ,
          development: ,
          lts: ,
          name: "",
          // Optional
          latestVersion: "5.2.4",
          latestReleaseDate: 2022-12-16,
          releaseDate: 
        }
      }
      
      // TODO: Find a better name
      // Whether active development is happening in this release cycle.
      // Use date for the last date of activeDevelopment.
      development: true/false/date
    }
  ]
}
```
