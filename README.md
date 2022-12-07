Case

When[Dim Date].[Hierarchy Fiscal Year Semester Quarter].CurrentMember.Level Is[Dim Date].[Hierarchy Fiscal Year Semester Quarter].[(All)]
Then "NA"

When IsEmpty
  (
    (
      ParallelPeriod(
        [Dim Date].[Hierarchy Fiscal Year Semester Quarter].[Fiscal Year], 1,
        [Dim Date].[Hierarchy Fiscal Year Semester Quarter].CurrentMember
      ),
      [Measures].[Units Balance]
    )
  )
Then Null
Else(
    ([Dim Date].[Hierarchy Fiscal Year Semester Quarter].CurrentMember,
      [Measures].[Units Balance]) -
    (
      ParallelPeriod(
        [Dim Date].[Hierarchy Fiscal Year Semester Quarter].[Fiscal Year],
        1,
        [Dim Date].[Hierarchy Fiscal Year Semester Quarter].CurrentMember
      ),
      [Measures].[Units Balance]
    )
  )
  /
  (
    ParallelPeriod(
      [Dim Date].[Hierarchy Fiscal Year Semester Quarter].[Fiscal Year],
      1,
      [Dim Date].[Hierarchy Fiscal Year Semester Quarter].CurrentMember
    ),
    [Measures].[Units Balance]
  )
End
