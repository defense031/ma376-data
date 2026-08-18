# Attribution

## package_data/sleuth3/
Extracted from the Sleuth3 R package, version 1.0-6, licensed GPL (>= 2).
Original by F. L. Ramsey and D. W. Schafer; modifications by Daniel W. Schafer,
Jeannie Sifneos and Berwin A. Turlach. Maintained by Berwin A. Turlach.
Source: https://cran.r-project.org/package=Sleuth3

These are the data for Ramsey, F. L. and Schafer, D. W., *The Statistical Sleuth:
A Course in Methods of Data Analysis* (3rd ed.), Cengage. The csv files here are a
verbatim export of the package's data frames; no values were changed.

## package_data/islr2/
Extracted from the ISLR2 R package, version 1.3-2, licensed GPL-2.
Gareth James, Daniela Witten, Trevor Hastie and Rob Tibshirani, with contributions
by Balasubramanian Narasimhan. Maintained by Trevor Hastie.
Source: https://cran.r-project.org/package=ISLR2 and https://www.statlearning.com

These are the data for James, Witten, Hastie and Tibshirani, *An Introduction to
Statistical Learning* (2nd ed.), Springer. The csv files here are a verbatim export
of the package's data frames; no values were changed.

Two ISLR2 objects are lists rather than tables and have no csv here: Khan and NCI60.
Load those from the package.

## Reading package_data back

In these files an EMPTY field means missing, so read them with

    read.csv(path, na.strings = "")

R would otherwise write missing as the token NA, which is indistinguishable from a
real value in Sleuth3's ex0918, where the factor level "NA" means North America.
One cost: ex0721 holds a single genuinely empty Name, which reads back as missing.

The files under project_data/ are byte-for-byte copies of the shipped csv files and
use R's ordinary conventions; read those with a plain read.csv(path).

## package_data/base/
From R's own datasets package, licensed GPL-2, part of the R distribution.
USArrests is the dataset ISLR's chapter-12 lab uses; it is base R, not ISLR2.
Row names are kept as the first csv column, since they are the state names.

The GPL-2 text every one of these points to is in LICENSE-GPL-2.

## project_data/
Each folder's DICTIONARY.md carries that dataset's own provenance, retrieval date,
and the license of every source merged into it.
