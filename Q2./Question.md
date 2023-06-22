Building project A outputs .pdb files useful for debugging the built application. Artifacts from this
build are used in the public release of the application. The developers want to omit the .pdb files
from the application but need to store them somewhere for debugging any issues which may be
logged after release. They would like to store these in an Amazon s3 bucket. Describe, using
examples, how you would approach this using GitHub Actions.