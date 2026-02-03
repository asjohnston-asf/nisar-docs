# Data Format: HDF5

## What is HDF5?
NISAR GCOV products are delivered in HDF5, or Hierarchical Data Format version 5. HDF5 is a file format designed to store, organize, and access large scientific datasets. GCOV uses HDF5 to systematically organize radar data and metadata in a way that is both efficient and easy to read, share, and analyze.

HDF was originally developed by the University of Illinois' National Center for Supercomputing Applications (NCSA) to support data sharing within the scientific community. HDF5 represents a significant redesign compared to earlier versions of HDF, with a more flexible and powerful internal structure. For additional details, users can consult the official HDF documentation at
<https://portal.hdfgroup.org/display/HDF5/HDF5>.


At a high level, an HDF5 file functions as a container that organizes data into a hierarchy of objects, such as **{abbr}`groups(A folder within an HDF5 file)`**, **{abbr}`datasets(The actual data values stored in an HDF5 file)`**, and **{abbr}`datatypes(The type and format of data)`**. In general, radar layers are organized **{abbr}`frequencyA(Lower portion of the radar bandwidth)`**/ and (potentially) **{abbr}`frequencyB(Higher portion of the radar signal)`**/. Note that nothing stored at the root `/`.


### Groups
An HDF5 **{abbr}`group(A folder within an HDF5 file)`** is a folder within an HDF5 file. Groups can hold datasets, datatypes, and other groups (subfolders). In essence, groups act like directories on computers. Path navigation is identical to that of Unix path navigation: `/`.

### Datasets
An HDF5 **{abbr}`dataset(A collection of data values stored in an HDF5 file)`** is where the actual data lives. This might be an array or table stored within the HDF5 file. Each dataset will include the data, a **{abbr}`dataspace(Describing the shape of the data)`**, a **{abbr}`datatype(What values are: integers, floats, etc)`**, and other optional attributes such as units, range, time, and other descriptions. 


### Attributes
An HDF5 **attribute** is a small piece of information that describes a **{abbr}`group(A folder within an HDF5 file)`** or **{abbr}`dataset(A collection of data values stored in an HDF5 file)`**. Note that an attribute does not store the data itself. Attributes provide important context that help correctly interpret values within a dataset. Common examples include:
- Units of measurement
- Descriptions of what the data represent
- Valid ranges, dates of acquisition
- Processing details
  
Storing this information with the data helps ensure that datasets can be understood and used correctly without relying on external documentation.

### Datatypes

An HDF5 datatype describes the kind of data that is being stored. A datatype explains both how to interpret a dataset and how it is stored. Datatypes are categorized into three types: **{abbr}`atomic datatypes(Basic building blocks)`**, **{abbr}`composite datatypes(Combinations of atomic types)`**, and **{abbr}`named datatypes(Ways of storing and sharing datatypes)`**. 
    
### Atomic Datatypes
**{abbr}`Atomic datatypes(Basic building blocks)`** are typically the simplest datatypes. They serve as building blocks for more complex datatypes. Common atomic datatypes include:
- Time
- Bitfield
- String
- Reference
- Opaque
- Integer
- Float

**{abbr}`Derived datatypes(Customized versions of atomic datatypes)`** are customized atomic types, commonly used for N-bit integers, floating-point formats, and other nonstandard data representations. They enable efficient and precise storage when data do not conform to standard numeric formats. Derived datatypes are useful because they: 
- Allow custom storage with specific bit lengths
- Support values that do not follow standard integer or floating-point formats
- Preserve the original format in which the data were recorded

### Composite Datatypes
**{abbr}`Composite datatypes(Combinations of atomic types)`** combine multiple atomic datatypes into more complex structures. Common composite datatypes include: 
- **{abbr}`Array datatypes(Fixed-size, multi-dimensional arrays treated as a single unit)`**
- **{abbr}`Variable-length datatypes(One-dimensional arrays whose length can vary between elements)`**
- **{abbr}`Compound datatypes(Collections of named fields, each with its own datatype)`**
- **{abbr}`Enumeration datatypes(Map integer values to named labels)`**


### Named Datatypes
**{abbr}`Named datatypes(Ways of storing and sharing datatypes)`** are stored as objects within an HDF5 file. Any datatype (atomic, derived, or composite) can be named or referenced throughout the file.
Naming allows datatypes to be:
- Shared across datasets and attributes
- Reused simply and consistently
