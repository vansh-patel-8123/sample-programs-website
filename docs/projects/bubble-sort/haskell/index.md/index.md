---

---

Welcome to the Bubble Sort in Haskell page! Here, you'll find the source code for this program as well as a description of how the program works.

## Current Solution

Note: The solution shown here is the current solution in the Sample Programs repository. Documentation below may be outdated.

```Haskell
module Main where

import Text.Read
import System.Environment
import System.Exit (exitWith, ExitCode(ExitFailure))
import Data.List (intercalate)


bubble :: Ord a => [a] -> [a]
bubble xs = foldl (\acc _ -> pass acc) xs xs
  where pass [x] = [x]
        pass (x1:x2:xs)
          | x1 > x2   = x2:(pass (x1:xs))
          | otherwise = x1:(pass (x2:xs))


headMaybe :: [a] -> Maybe a
headMaybe []     = Nothing
headMaybe (x:xs) = Just x

-- Converts string in format "1, 2, 3" to a Maybe list of int
stringToListMaybe :: String -> Maybe [Int]
stringToListMaybe str = readMaybe $ "[" ++ str ++ "]" :: Maybe [Int]

-- Ensure that a list contains at least two elements
verifyListLength :: Ord a => [a] -> Maybe [a]
verifyListLength []     = Nothing
verifyListLength [x]    = Nothing
verifyListLength (x:xs) = Just (x:xs)

listToString :: [Int] -> String
listToString = intercalate ", " . map show


main :: IO ()
main = do
  args <- getArgs
  let xs = headMaybe args >>= stringToListMaybe >>= verifyListLength
  case xs of
    Nothing -> do
      putStrLn "Usage: please provide a list of at least two integers to sort in the format \"1, 2, 3, 4, 5\""
      exitWith $ ExitFailure 1
    Just xs  -> putStrLn $ listToString $ bubble xs


```

## How to Implement the Solution

No how to implement the solution available. Please consider contributing.

## How to Run the Solution

No how to run the solution available. Please consider contributing.