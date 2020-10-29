# oso / NestJS integration

This repository contains experimental work on a oso NestJS plugin,
based on previous work done in the example application:
[Document Management with NestJS and oso](https://github.com/osohq/oso-nest-doc-mgmt).

# (Target) Features

## Route-level authorization

"Is the current user allowed to call this endpoint for this resource".
E.g. `GET /documents/1` - is the user allowed to read documents.

Handled in the [example app](https://github.com/osohq/oso-nest-doc-mgmt/blob/d988109cd6fbd90a2c3b95c51975ef2fb776782a/src/oso/oso.guard.ts#L37)
by using a controller-level guard.

Two possible modes:
- Require all routes to have authorization or explicitly opt-out
- Opt-in to route-level authorization

## Resource-level authorization

"Is the current user allowed to perform this action on this specific resource"
E.g. should the method `this.documentService.create(document);` be allowed?

Handled in the [example app](https://github.com/osohq/oso-nest-doc-mgmt/blob/main/src/document/document.controller.ts#L55)
by using a custom guard providing an `authorize` method.

## oso lifecycle + policy loading

- A single global instance of oso [example](https://github.com/osohq/oso-nest-doc-mgmt/blob/main/src/oso/oso-instance.ts#L10)
- Load policy files [example](https://github.com/osohq/oso-nest-doc-mgmt/blob/main/src/oso/oso-instance.ts#L28-L29)
- Register classes with oso [example](https://github.com/osohq/oso-nest-doc-mgmt/blob/main/src/oso/oso-instance.ts#L17-L26)
- (Nice-to-have) reload on changes to policy files
- (Nice-to-have) Automatically register all classes
