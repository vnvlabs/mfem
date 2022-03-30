ARG FROM_IMAGE=vnv_petsc
FROM ${FROM_IMAGE}:latest

#Install MOOSE with VnV
COPY . ./mfem 
RUN cd mfem && mkdir docker_build && cd docker_build && cmake -DHYPRE_DIR=${HYPRE_DIR} -DMETIS_DIR=${PETSC_DIR} -DPETSC_DIR=${PETSC_DIR} -DPETSC_ARCH=${PETSC_ARCH} -DInjection_DIR=${VNV_DIR}/lib/cmake/ -DMFEM_USE_PETSC=ON -DMFEM_USE_VNV=ON -DCMAKE_EXPORT_COMPILE_COMMANDS=ON -DBUILD_SHARED_LIBS=ON  -DCMAKE_INSTALL_PREFIX=/root/software/mfem .. && make && make install

ARG COMMIT_HASH=unknown
LABEL vnv.version.mfem=${COMMIT_HASH}




ENV VNV_CONFIG=${VNV_CONFIG}:/mfem/.vnv-config.json



