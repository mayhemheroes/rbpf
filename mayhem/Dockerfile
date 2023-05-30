FROM fuzzers/cargo-fuzz:0.11.0 as builder
#RUN rustup toolchain install nightly

ADD . /rbpf
WORKDIR /rbpf

RUN cd fuzz/ && cargo fuzz build

FROM ubuntu:22.04
COPY --from=builder /rbpf/fuzz/target/x86_64-unknown-linux-gnu/release/dumb /
COPY --from=builder /rbpf/fuzz/target/x86_64-unknown-linux-gnu/release/smart /
COPY --from=builder /rbpf/fuzz/target/x86_64-unknown-linux-gnu/release/smart-jit-diff /
COPY --from=builder /rbpf/fuzz/target/x86_64-unknown-linux-gnu/release/smarter-jit-diff /
COPY --from=builder /rbpf/fuzz/target/x86_64-unknown-linux-gnu/release/verify-semantic-aware /
