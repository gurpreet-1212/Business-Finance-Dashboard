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
    subgraph "Final Data & Calculations"
        U -->|Combine costs for profit analysis| V[Create Comprehensive Financials DataFrame];
        V --> W[Include Customer Group & Channel Spends];
        W --> X[Visibility Metrics Incorporated];
        X --> Y[Use Pivot Tables for Maximum Values];
        Y -->|Resolve duplicates & ensure latest values| Z[Create Pivoted DataFrame];
        Z --> A1[Pass Data if Duplicates Found];
        A1 --> B1[Merge Processed File with Master Data];
        B1 --> C1[Calculate Marketing Spends & Other Financial Factors];
        C1 -->|Finalize calculations| D1[Create Final Processed DataFrame];
        D1 --> E1[Handle Null Values];
        E1 --> F1[Calculate Key Percentages];
        F1 --> G1[Merge Freight Lines];
        G1 -->|Ensure complete financial overview| H1[Create Final Business Finance DataFrame];
    end

    subgraph "Dashboard & Reporting"
        H1 --> I1[Final Financial & Business Insights Dashboard];
        I1 --> J1[Generate Reports & Visualizations];
        J1 --> K1[End: Dashboard Ready for Analysis];
    end
