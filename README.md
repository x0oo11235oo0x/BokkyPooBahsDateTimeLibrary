# BokkyPooBah's DateTime Library

## Table Of Contents

* [References](#references)

<br />

<hr />

## Algorithm

From [Converting Between Julian Dates and Gregorian Calendar Dates](http://aa.usno.navy.mil/faq/docs/JD_Formula.php):

### Converting YYYYMMDD to Unix Timestamp

```
    INTEGER FUNCTION JD (YEAR,MONTH,DAY)
C
C---COMPUTES THE JULIAN DATE (JD) GIVEN A GREGORIAN CALENDAR
C   DATE (YEAR,MONTH,DAY).
C
    INTEGER YEAR,MONTH,DAY,I,J,K
C
    I= YEAR
    J= MONTH
    K= DAY
C
    JD= K-32075+1461*(I+4800+(J-14)/12)/4+367*(J-2-(J-14)/12*12)
   2    /12-3*((I+4900+(J-14)/12)/100)/4
C
    RETURN
    END
```

Translating this formula

```
    days = dd - 32075 + 1461*(yyyy+4800+(mm-14)/12)/4+367*(mm-2-(mm-14)/12*12)/12-3*((yyyy+4900+(mm-14)/12)/100)/4
```

<br />

### Converting Unix Timestamp To YYYYMMDD

```
    SUBROUTINE GDATE (JD, YEAR,MONTH,DAY)
C
C---COMPUTES THE GREGORIAN CALENDAR DATE (YEAR,MONTH,DAY)
C   GIVEN THE JULIAN DATE (JD).
C
    INTEGER JD,YEAR,MONTH,DAY,I,J,K
C
    L= JD+68569
    N= 4*L/146097
    L= L-(146097*N+3)/4
    I= 4000*(L+1)/1461001
    L= L-1461*I/4+31
    J= 80*L/2447
    K= L-2447*J/80
    L= J/11
    J= J+2-12*L
    I= 100*(N-49)+I+L
C
    YEAR= I
    MONTH= J
    DAY= K
C
    RETURN
    END
 ```

## References


<br />

<br />

(c) BokkyPooBah / Bok Consulting Pty Ltd - May 23 2018. [GNU Lesser General Public License 3.0](https://www.gnu.org/licenses/lgpl-3.0.en.html)