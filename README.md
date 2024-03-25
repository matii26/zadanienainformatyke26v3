# zadanienainformatyke26v3

def zadanie_3_1():
    with open('pi.txt', 'r') as file:
        digits = file.read().replace('\n', '')
    two_digit_fragments = [int(digits[i:i+2]) for i in range(len(digits)-1)]
    return len([fragment for fragment in two_digit_fragments if fragment > 90])


def zadanie_3_2():
    with open('pi.txt', 'r') as file:
        digits = file.read().replace('\n', '')
    two_digit_fragments = [digits[i:i+2] for i in range(len(digits)-1)]
    fragment_counts = {str(i).zfill(2): two_digit_fragments.count(str(i).zfill(2)) for i in range(100)}
    min_fragment = min(fragment_counts, key=fragment_counts.get)
    max_fragment = max(fragment_counts, key=fragment_counts.get)
    return min_fragment, fragment_counts[min_fragment], max_fragment, fragment_counts[max_fragment]


    def zadanie_3_3():
    with open('pi.txt', 'r') as file:
        digits = file.read().replace('\n', '')
    six_digit_sequences = [digits[i:i+6] for i in range(len(digits)-5)]
    increasing_decreasing_sequences = [seq for seq in six_digit_sequences if is_increasing_decreasing(seq)]
    return len(increasing_decreasing_sequences)

def is_increasing_decreasing(sequence):
    increasing_part = list(takewhile(lambda pair: pair[0] < pair[1], pairwise(sequence)))
    if len(increasing_part) < 2 or len(increasing_part) == len(sequence) - 1:
        return False
    decreasing_part = sequence[len(increasing_part):]
    return all(pair[0] > pair[1] for pair in pairwise(decreasing_part))

def pairwise(iterable):
    a, b = tee(iterable)
    next(b, None)
    return zip(a, b)



def zadanie_3_4():
    with open('pi.txt', 'r') as file:
        digits = file.read().replace('\n', '')
    sequences = [digits[i:j+1] for i in range(len(digits)) for j in range(i+3, len(digits))]
    increasing_decreasing_sequences = [(i, seq) for i, seq in enumerate(sequences) if is_increasing_decreasing(seq)]
    max_length_sequence = max(increasing_decreasing_sequences, key=lambda x: len(x[1]))
    return max_length_sequence



with open('wyniki3.txt', 'w') as file:
    file.write(f'3.1\n{zadanie_3_1()}\n')
    min_fragment, min_count, max_fragment, max_count = zadanie_3_2()
    file.write(f'3.2\n{min_fragment} {min_count}\n{max_fragment} {max_count}\n')
    file.write(f'3.3\n{zadanie_3_3()}\n')
    start_position, sequence = zadanie_3_4()
    file.write(f'3.4\n{start_position}\n{sequence}\n')
