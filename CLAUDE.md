# rac-ca

**THE home for Canadian federal and provincial tax/benefit statute encodings.**

All Canada-specific .rac files belong here, NOT in rac-compile.

## Structure

Files organized under `statute/` by act and section:

```
rac-ca/
├── statute/                    # All enacted statutes
│   ├── ITA/                   # Income Tax Act (R.S.C., 1985, c. 1 (5th Supp.))
│   │   ├── 122.5/             # GST/HST Credit
│   │   ├── 122.6/             # Canada Child Benefit definitions
│   │   ├── 122.61/            # Canada Child Benefit calculation
│   │   ├── 122.7/             # Canada Workers Benefit
│   │   ├── 122.8/             # Climate Action Incentive Payment
│   │   └── 122.9/             # Provincial tax credits
│   │
│   ├── OAS/                   # Old Age Security Act (R.S.C., 1985, c. O-9)
│   │   ├── 3/                 # OAS pension eligibility
│   │   ├── 11/                # OAS pension amount
│   │   ├── 12/                # Guaranteed Income Supplement
│   │   ├── 19/                # Allowance
│   │   └── 22/                # Recovery tax (clawback)
│   │
│   ├── EI/                    # Employment Insurance Act (S.C. 1996, c. 23)
│   │   ├── 5/                 # Insurable employment
│   │   ├── 6/                 # Benefits qualification
│   │   ├── 14/                # Benefit rate
│   │   ├── 67/                # Premium rate
│   │   └── 68/                # Maximum insurable earnings
│   │
│   └── provincial/            # Provincial programs
│       ├── ON/                # Ontario
│       │   └── ow/            # Ontario Works
│       ├── BC/                # British Columbia
│       │   └── hb/            # BC Housing Benefit
│       ├── AB/                # Alberta
│       │   └── fess/          # Family Employment Support Services
│       └── QC/                # Quebec
│           └── solidarity/    # Solidarity Tax Credit
│
├── cra/                       # CRA guidance (benefit tables, etc.)
│   └── ccb-fy2024/           # CCB payment tables
│       └── parameters.yaml
│
└── tests/
    └── integration/
        └── complete_benefit_test.yaml
```

## Canadian Tax/Benefit Structure

### Federal Benefits (Income Tax Act)

| Section | Program | Description |
|---------|---------|-------------|
| 122.5 | GST/HST Credit | Quarterly payment to offset sales tax |
| 122.6/122.61 | Canada Child Benefit (CCB) | Monthly tax-free payment for children |
| 122.7 | Canada Workers Benefit (CWB) | Refundable credit for low-income workers |
| 122.8 | Climate Action Incentive Payment (CAIP) | Carbon tax rebate |

### Old Age Security Programs

| Section | Program | Description |
|---------|---------|-------------|
| 3, 11 | OAS Pension | Monthly payment for seniors 65+ |
| 12 | GIS | Income-tested supplement for low-income seniors |
| 19 | Allowance | For spouses/partners of GIS recipients |
| 22 | Recovery Tax | Clawback for high-income seniors |

## References in .rac files

Cross-file references use paths relative to the repo root:
```
references {
  adjusted_family_net_income: statute/ITA/122.6/adjusted_family_net_income
  num_children: statute/ITA/122.61/num_qualified_dependants
}
```

## Key Canadian Concepts

### Adjusted Family Net Income (AFNI)
Most federal benefits use AFNI (line 23600 + line 23600 of spouse) as the income test.

### Qualified Dependant
For CCB: child under 18 for whom you are primarily responsible.

### Benefit Years
- CCB: July to June (based on prior year income)
- GST/HST Credit: July to June quarterly
- OAS/GIS: Annual, quarterly adjustments

## Authoritative Sources

- **Laws**: https://laws-lois.justice.gc.ca/
- **Income Tax Act**: https://laws-lois.justice.gc.ca/eng/acts/I-3.3/
- **Old Age Security Act**: https://laws-lois.justice.gc.ca/eng/acts/O-9/
- **EI Act**: https://laws-lois.justice.gc.ca/eng/acts/E-5.6/
- **CRA Benefits**: https://www.canada.ca/en/revenue-agency/services/child-family-benefits.html

## File Types

- `.rac` - Executable formulas (compile to Python/JS/WASM)
- `parameters.yaml` - Time-varying values (rates, thresholds, amounts)
- `tests.yaml` - Validation test cases

## Related Repos

- **atlas** - Source document archive (R2) + catalog
- **rac-validators** - Validation against external calculators
- **rac-compile** - DSL compiler and runtime
