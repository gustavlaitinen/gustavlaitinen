Case

When [Dim Date].[HierarchyFiscalYearSemesterQuarter].CurrentMember.Level Is
[DimDate].[HierarchyFiscalYearSemesterQuarter].[(All)]
Then "NA"

When IsEmpty
(
(
ParallelPeriod
(
[DimDate].[HierarchyFiscalYearSemesterQuarter].[Fiscal Year],1,
[DimDate].[HierarchyFiscalYearSemesterQuarter].CurrentMember
),
[Measures].[UnitsBalance]
)
)
Then Null
Else (
([DimDate].[HierarchyFiscalYearSemesterQuarter].CurrentMember,
[Measures].[UnitsBalance])
-
(
ParallelPeriod
(
[DimDate].[HierarchyFiscalYearSemesterQuarter].[FiscalYear],
1,
[DimDate].[HierarchyFiscalYearSemesterQuarter].CurrentMember
),
[Measures].[UnitsBalance]
)
)
/
(
ParallelPeriod
(
[DimDate].[HierarchyFiscalYearSemesterQuarter].[FiscalYear],
1,
[DimDate].[HierarchyFiscalYearSemesterQuarter].CurrentMember
),
[Measures].[UnitsBalance]
)
End
