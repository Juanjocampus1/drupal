# File Example

This example contains examples demonstrating the Drupal File API. The
File Example module is part of the Examples for Developers Project and
provides a variety of examples for the Developers project page.

## Examples in this module

The module demonstrates the following concepts:

* Creating, moving, and deleting files, and reading and writing from them.
* Using files that Drupal can manage via its Entity API ("managed files"),
  and unmanaged files (the usual kind of file programs deal with).
* Creating and setting up directories with the right permissions, and with
  .htaccess files that prevent unwanted accesses.
* Allowing restricted access to files the way Drupal private files are
  downloaded.
* Using special "stream" URIs like `public://`, `private://`, and
  `temporary://`. Drupal has good support for this PHP language feature. You
  can implement new file schemes as well; see the Stream Wrapper Example for
  how to do that. If you enable the `stream_wrapper_example` module, you can
  use it together with the File Example to test how a custom stream works.

To demonstrate all of this, the File Example implements a form that lets you
play with files. Read `src/Form/FileExampleReadWriteForm.php` to see
demonstrations of the various File API functions you will want to use in your
code.

## hook_file_download()

Implements `hook_file_download()` to allow modules to enforce permissions on
file downloads. The function checks the permission of the current user and
returns an array with appropriate headers if the user has permission to
access the file. If the user does not have permission to access the file,
the function returns -1. If the file is not controlled by the current
module, the return value should be NULL.

To have `hook_file_download()` called, the code needs to set up the routes
so that the download link uses `FileDownloadController::download()` as a
controller. `FileDownloadController::download()` enforces access restrictions
on the files it manages, in part by invoking `hook_file_downloads()`. See
the File Example's routing file to see how to do this.
