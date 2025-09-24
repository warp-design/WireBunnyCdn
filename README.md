# WireBunnyCdn

A ProcessWire module that provides offloading of images/files to Bunny Storage and rewriting URLs to a Bunny CDN domain whilst retaining core ProcessWire image/file handling and sizing functionality.

## Features

* Zero template changes – hooks Pagefile::url() to return CDN URLs.

* Offload on save – uploads originals and image variations to Bunny Storage, and mirrors local assets folder structure.

* Immediate variation upload – after Pageimage::size().

* Removes remote files when deleted locally (and on page delete).

* Prefer local files (optional) – return local URLs if files already exist on local hosting - e.g if they were added to the site before the CDN was implemented.

* Supports use of Bunny Optimizer mode (optional) – rewrite sized URLs to ?width=&height= on the original, served by the CDN. Or use ProcessWire default size(X,X) methods.

## Requirements

* ProcessWire 3.0.150+

* PHP cURL

* Bunny.net account with:
    * Storage Zone (name + Password)
    * CDN hostname (Pull Zone connected to Storage, or Storage CDN host)* (Optional) Bunny Optimizer enabled if using Optimizer mode

## Installation

1) Copy module to:

    `/site/modules/WireBunnyCdn/`


2) In the admin: Modules → Refresh → Install “WireBunnyCdn”.

## Configuration/Options (module settings)

* CDN domain – your CDN host (Pull Zone or Storage CDN hostname), e.g. https://cdn.example.com.

* Offload to Bunny Storage – enable uploads to Storage.

* Storage Zone – exact zone name.

* Storage Access Key – the Storage Zone Password (not the read only password).

* Storage Region – optional (e.g. uk) - if not specifying, endpoint must contain region.

* Prefer local URL if file exists – return local URLs when present.

* Use Bunny Optimizer for sized URLs – rewrite image.800x600.jpg to original + ?width=800&height=600 or leave off for standard ProcessWire sizing behaviour.

## Usage

No template changes needed:

**Original**
`echo $page->images->first()->url;`

**Sized**
`echo $page->image_field->size(800, 600)->url;`

_With Optimizer mode ON, sized calls become original + query params served by the CDN._

_With Optimizer mode OFF, ProcessWire creates local variations which are then uploaded and served from the CDN._

## Notes

* Admin and front-end image URLs are rewritten to the CDN.

* Local copies are retained by default (safe mirroring).


## Roadmap

* Handling of video uploads, possibly to a seperate Bunny Stream endpoint.
* Chunked/background uploading (via CRON) for big files - e.g. videos.

## Contributing

Issues and PRs welcome.