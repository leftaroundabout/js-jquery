# js-jquery [![Hackage version](https://img.shields.io/hackage/v/js-jquery.svg?label=Hackage)](https://hackage.haskell.org/package/js-jquery) [![Build Status](https://img.shields.io/travis/ndmitchell/js-jquery.svg)](https://travis-ci.org/ndmitchell/js-jquery)

This package bundles the minified [jQuery](http://jquery.com/) code into a Haskell package,
so it can be depended upon by Cabal packages. The first three components of
the version number match the upstream jQuery version. The package is designed
to meet the redistribution requirements of downstream users (e.g. Debian).
As an example:

```haskell
import qualified Language.Javascript.JQuery as JQuery

main = do
    putStrLn $ "jQuery version " ++ show JQuery.version ++ " source:"
    putStrLn =<< readFile =<< JQuery.file
```

This package installs data files containing the jQuery sources, which must be available at runtime. If you want to produce an executable with no dependency on associated data files, you can use the [`file-embed`](https://hackage.haskell.org/package/file-embed) library:

```haskell
{-# LANGUAGE TemplateHaskell #-}

import Data.FileEmbed
import qualified Data.ByteString as BS
import qualified Language.Javascript.JQuery as JQuery
import Language.Haskell.TH.Syntax

main = print jQueryContents

jQueryContents :: BS.ByteString
jQueryContents = $(embedFile =<< runIO JQuery.file)
```
