```mermaid
graph TD

    A[Start: Business Finance Dashboard] --> B[Load Sales Register Dataset];

    subgraph "Customer Data"
        B -->|Get customer attributes| C[Import Customer Master Data];
        C --> D[Stage Customer Data & Merge with Sales Register];
        D -->|Link customer details with sales| E[Create Merged Customer-Sales DataFrame];
    end

    subgraph "Product Data"
        B -->|Get product MRP| F[Import Product Master Data];
        F --> G[Extract Product Details];
        G -->|Add product metadata to transactions| H[Create Product Details DataFrame];
        H --> I[Merge Product Items with Base Dataset];
        I --> J[Add Category, Sub-category, and Brand Information];
        J -->|Enable category-wise sales & cost analysis| K[Create Categorized Sales DataFrame];
    end

    subgraph "Cost Metrics"
        K --> L[Extract Cost Metrics];
        L --> M[DPC Cost Calculation];
        M -->|Essential for cost analysis| N[Create Cost Analysis DataFrame];
        N --> O[Reset Logistics & Packaging Costs];
        O -->|Separate costs for accuracy| P[Create Cost Adjustments DataFrame];
    end

    subgraph "AMP Spends"
        P --> Q[Import AMP Spends Data];
        Q --> R[Merge AMP Spends for DPL Calculation];
        R -->|Capture marketing costs| S[Create AMP Spends DataFrame];
    end

    %% --- MERGE ALL DATAFRAMES --- %%
    E & K & P & S --> T{Merge all dataframes?};

    T -- Yes --> U[Create Final DataFrame];

    %% --- FINAL STEPS --- %%
    U -->|Combine costs for profit analysis| V[Create Comprehensive Financials DataFrame];
    V --> W[Include Customer Group & Channel Spends];
    W --> X[Visibility Metrics Incorporated];
    X --> Y[Use Pivot Tables for Maximum Values];
    Y -->|Resolve duplicates & ensure latest values| Z[Create Pivoted DataFrame];
    Z --> A1[Pass Data if Duplicates Found];
    A1 --> B1[Merge Processed File with Master Data];
    B1 --> C1[Calculate Marketing Spends & Other Financial Factors];
    C1 -->|Derive KPIs and ratios| D1[Calculate Factors];
    D1 -->|Finalize calculations| E1[Create Final Processed DataFrame];
    E1 --> F1[Handle Null Values];
    F1 --> G1[Calculate Key Percentages];
    G1 --> H1[Merge Freight Lines];
    H1 -->|Ensure complete financial overview| I1[Create Final Business Finance DataFrame];

    I1 --> J1[Final Financial & Business Insights Dashboard];
    J1 --> K1[Generate Reports & Visualizations];
    K1 --> L1[End: Dashboard Ready for Analysis];
