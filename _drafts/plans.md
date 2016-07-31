# Use enums to map information

All information that is known in compile time should be defined in compile time and not in runtime.

Information belonging together should be statically mapped. Else other methods will be polluted by mapping them. It is not their responsibility.

# Service Classes Must Be Facades
