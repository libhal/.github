<div align="center">
<img height="250" src="https://raw.githubusercontent.com/libhal/.github/main/profile/logo.png">
<br />
<br />

```
🚚 portable 🦾 flexible 📦 accessible 🍰 easy to use
```
<br />
</div>

<div align="center">

[![GitHub stars](https://img.shields.io/github/stars/libhal/libhal.svg)](https://github.com/libhal/libhal/stargazers)
[![Discord](https://img.shields.io/discord/800515757871726622?color=7389D8&logo=discord&logoColor=ffffff&labelColor=6A7EC2)](https://discord.gg/p5A6vzv8tm)

[Install](#-install)
| [Overview](#ℹ%EF%B8%8F-overview)
| [Getting Started](#-getting-started-incomplete)
| [Badges](#-library-badges)
| [Libraries](#-libraries)
| [Motivation](#-motivation)
| [Glossary](#-glossary)

🚧 **_This document is still in construction and is subject to change at any time_** 🚧

</div>

# [📚 libhal APIs](https://libhal.github.io/libhal/api)

# 📥 Install

Libhal is simply a set of interfaces for hardware drivers. It can be adopted in
many ways, one of which is simply downloading the header only library and using
the interfaces directly, but this will not give as much of a benefit without a
package manager to make managing, upgrading, and changing dependencies easier.

## Using Conan (RECOMMENDED)

Link to the [Install Conan Prerequisites](docs/conan-setup.md) page.

### Install from `libhal-trunk`

`libhal-trunk` is a remote conan server with the latest version of the code.

Run the following to add `libhal-trunk` to your list of conan remote servers.

NOTE: that the `--insert` argument places this server at the highest priority
for conan, meaning updates will be checked at this server first before
attempting to check out servers like the CCI.

```bash
conan remote add libhal-trunk https://libhal.jfrog.io/artifactory/api/conan/trunk-conan --insert
conan config set general.revisions_enabled=True
```

### Create conan package locally

```bash
git clone https://github.com/libhal/libhal.git
cd libhal
conan create .
```

# ℹ️ Overview

libhal exists to make hardware drivers:

- **🚚 portable**
- **🦾 flexible**
- **📦 accessible**
- **🍰 easy to use**

## Project Attributes

- Header only
- Available on Conan (coming soon to vcpkg)
- Does not throw exceptions
- Does not dynamically allocate
- Uses tweak header files for customization
- Designed to be modular, dynamic, composable, and lightweight
- System agnostic
- Follows C++ Core Guidelines
- Dependencies:
  - C++20
  - [Boost.LEAF](https://boostorg.github.io/leaf/) for error handling

# 🚀 Getting Started

Check out the [libhal-starter](https://github.com/libhal/libhal-starter) project
to get started with libhal.