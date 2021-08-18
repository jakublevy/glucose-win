# Windows builds for The Glucose SAT Solver
Glucose is based on a new scoring scheme for the clause learning mechanism of so called "Modern" SAT solvers (it is based on [this paper](https://www.ijcai.org/Proceedings/09/Papers/074.pdf)). 

Glucose is designed to be parallel since 2014. The name of the Solver is a contraction of the concept of "glue clauses", a particular kind of clauses that glucose detects and preserves during search.

## Directory Overview
| Directory      | Description |
| ----------- | ----------- |
| [mtl/](mtl/)           | Minisat Template Library                                                  |
| [core/](core/)         | A core version of the solver                                              |
| [simp/](simp/)         | An extended single-core solver with simplification capabilities (glucose) |
| [parallel/](parallel/) | A multi-core version of glucose called glucose-syrup                      |

## Building
```
$ cd { simp | parallel }
$ make rs
```

## Installation
### Chocolatey
Glucose is available as a Chocolatey package [glucose](https://community.chocolatey.org/packages/glucose). Install by executing
```
> choco install glucose
```

### Manual
Grab [the latest release](https://github.com/jakublevy/glucose-win/releases) and put it somewhere on your computer.

## Usage
For the single-core solver:
```
> glucose --help
c
c This is glucose 4.1 --  based on MiniSAT (Many thanks to MiniSAT team)
c
c USAGE: glucose.exe [options] <input-file> <result-output-file>

  where input may be either in plain or gzipped DIMACS.

CORE OPTIONS:

  -forceunsat, -no-forceunsat             (default: on)
  -adapt, -no-adapt                       (default: on)
  -fix-phas-rest, -no-fix-phas-rest       (default: off)
  -luby, -no-luby                         (default: off)
  -gr, -no-gr                             (default: on)
  -rnd-init, -no-rnd-init                 (default: off)

  -gc-frac      = <double> (   0 ..  inf) (default: 0.2)
  -rinc         = <double> (   1 ..  inf) (default: 2)
  -rnd-seed     = <double> (   0 ..  inf) (default: 9.16483e+07)
  -rnd-freq     = <double> [   0 ..    1] (default: 0)
  -cla-decay    = <double> (   0 ..    1) (default: 0.999)
  -max-var-decay = <double> (   0 ..    1) (default: 0.95)
  -var-decay    = <double> (   0 ..    1) (default: 0.8)

  -phase-restart = <int32>  [   0 ..    3] (default: 0)
  -phase-saving = <int32>  [   0 ..    2] (default: 2)
  -ccmin-mode   = <int32>  [   0 ..    2] (default: 2)

CORE -- CERTIFIED UNSAT OPTIONS:

  -certified, -no-certified               (default: off)
  -vbyte, -no-vbyte                       (default: off)

  -certified-output = <string>

CORE -- MINIMIZE OPTIONS:

  -minLBDMinimizingClause = <int32>  [   3 .. imax] (default: 6)
  -minSizeMinimizingClause = <int32>  [   3 .. imax] (default: 30)

CORE -- REDUCE OPTIONS:

  -chanseok, -no-chanseok                 (default: off)

  -firstReduceDB = <int32>  [   0 .. imax] (default: 2000)
  -incReduceDB  = <int32>  [   0 .. imax] (default: 300)
  -luby-factor  = <int32>  [   1 .. imax] (default: 100)
  -minLBDFrozenClause = <int32>  [   0 .. imax] (default: 30)
  -specialIncReduceDB = <int32>  [   0 .. imax] (default: 1000)
  -co           = <int32>  [   2 .. imax] (default: 5)

CORE -- RESTART OPTIONS:

  -K            = <double> (   0 ..    1) (default: 0.8)
  -R            = <double> (   1 ..    5) (default: 1.4)

  -szLBDQueue   = <int32>  [  10 .. imax] (default: 50)
  -szTrailQueue = <int32>  [  10 .. imax] (default: 5000)

MAIN OPTIONS:

  -pre, -no-pre                           (default: on)
  -model, -no-model                       (default: off)

  -mem-lim      = <int32>  [   0 .. imax] (default: 2147483647)
  -verb         = <int32>  [   0 ..    2] (default: 1)
  -cpu-lim      = <int32>  [   0 .. imax] (default: 2147483647)
  -vv           = <int32>  [   1 .. imax] (default: 10000)

  -dimacs     = <string>

SIMP OPTIONS:

  -elim, -no-elim                         (default: on)
  -rcheck, -no-rcheck                     (default: off)
  -asymm, -no-asymm                       (default: off)

  -simp-gc-frac = <double> (   0 ..  inf) (default: 0.5)

  -grow         = <int32>  [imin .. imax] (default: 0)
  -sub-lim      = <int32>  [  -1 .. imax] (default: 1000)
  -cl-lim       = <int32>  [  -1 .. imax] (default: 20)

HELP OPTIONS:

  --help        Print help message.
  --help-verb   Print verbose help message.
```

For the multi-core solver:
```
> glucose-syrup --help
c
c This is glucose-syrup 4.1 (glucose in many threads) --  based on MiniSAT (Many thanks to MiniSAT team)
c
c USAGE: glucose-syrup.exe [options] <input-file> <result-output-file>

  where input may be either in plain or gzipped DIMACS.

CORE OPTIONS:

  -rnd-init, -no-rnd-init                 (default: off)
  -gr, -no-gr                             (default: on)
  -luby, -no-luby                         (default: off)
  -fix-phas-rest, -no-fix-phas-rest       (default: off)
  -adapt, -no-adapt                       (default: on)
  -forceunsat, -no-forceunsat             (default: on)

  -rinc         = <double> (   1 ..  inf) (default: 2)
  -gc-frac      = <double> (   0 ..  inf) (default: 0.2)
  -rnd-seed     = <double> (   0 ..  inf) (default: 9.16483e+07)
  -rnd-freq     = <double> [   0 ..    1] (default: 0)
  -cla-decay    = <double> (   0 ..    1) (default: 0.999)
  -max-var-decay = <double> (   0 ..    1) (default: 0.95)
  -var-decay    = <double> (   0 ..    1) (default: 0.8)

  -ccmin-mode   = <int32>  [   0 ..    2] (default: 2)
  -phase-restart = <int32>  [   0 ..    3] (default: 0)
  -phase-saving = <int32>  [   0 ..    2] (default: 2)

CORE -- MINIMIZE OPTIONS:

  -minSizeMinimizingClause = <int32>  [   3 .. imax] (default: 30)
  -minLBDMinimizingClause = <int32>  [   3 .. imax] (default: 6)

CORE -- REDUCE OPTIONS:

  -chanseok, -no-chanseok                 (default: off)

  -co           = <int32>  [   2 .. imax] (default: 5)
  -minLBDFrozenClause = <int32>  [   0 .. imax] (default: 30)
  -specialIncReduceDB = <int32>  [   0 .. imax] (default: 1000)
  -incReduceDB  = <int32>  [   0 .. imax] (default: 300)
  -firstReduceDB = <int32>  [   0 .. imax] (default: 2000)
  -luby-factor  = <int32>  [   1 .. imax] (default: 100)

CORE -- RESTART OPTIONS:

  -K            = <double> (   0 ..    1) (default: 0.8)
  -R            = <double> (   1 ..    5) (default: 1.4)

  -szLBDQueue   = <int32>  [  10 .. imax] (default: 50)
  -szTrailQueue = <int32>  [  10 .. imax] (default: 5000)

CORE/PARALLEL -- UNSTABLE FEATURES OPTIONS:

  -plingeling, -no-plingeling             (default: off)
  -reusedClauses, -no-reusedClauses       (default: off)

MAIN OPTIONS:

  -pre, -no-pre                           (default: on)
  -model, -no-model                       (default: off)

  -verb         = <int32>  [   0 ..    2] (default: 1)
  -vv           = <int32>  [   1 .. imax] (default: 10000)
  -cpu-lim      = <int32>  [   0 .. imax] (default: 2147483647)
  -mem-lim      = <int32>  [   0 .. imax] (default: 2147483647)

PARALLEL OPTIONS:

  -removeolder, -no-removeolder           (default: off)

  -maxmemory    = <int32>  [imin .. imax] (default: 20000)
  -statsinterval = <int32>  [imin .. imax] (default: 5)
  -maxnbthreads = <int32>  [imin .. imax] (default: 4)
  -fifosize     = <int32>  [imin .. imax] (default: 100000)
  -nthreads     = <int32>  [imin .. imax] (default: 0)

SIMP OPTIONS:

  -asymm, -no-asymm                       (default: off)
  -rcheck, -no-rcheck                     (default: off)
  -elim, -no-elim                         (default: on)

  -simp-gc-frac = <double> (   0 ..  inf) (default: 0.5)

  -cl-lim       = <int32>  [  -1 .. imax] (default: 20)
  -sub-lim      = <int32>  [  -1 .. imax] (default: 1000)
  -grow         = <int32>  [imin .. imax] (default: 0)

HELP OPTIONS:

  --help        Print help message.
  --help-verb   Print verbose help message.
```

## For more information about Glucose see [the official page](https://www.labri.fr/perso/lsimon/glucose).